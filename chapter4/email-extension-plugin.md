EMail extension plugin
====

在 build 的結果有失敗的時候, 我們會希望系統能自動寄信通知, 其實 Jenkins 本身已經有這個功能

首先進到 ```Configure System``` 裡面的 ```E-mail Notification``` 區域, 設定 SMTP 的 server 等等設定

![](/assets/email setting.PNG)

按下 ```Advanced``` 可以作更 detail 的設定

> 這裡就不提 SMTP 怎麼設定了, 不同的 SMTP server 跟用的 port 可能不一樣, 可能需要自己去 google 了

那在設定完之後, 到 job 的組態設定頁面, 新增個建置後事件, 選擇 ```E-mail Notification```

![](/assets/build mail setting.PNG)

就可以設定建置完寄信給誰了, 基本是 jenkins 預設的寄信條件是 (按問號就會寫以下內容)

```bash
1. 每次建置失敗都會觸發寄送新郵件。
2. 建置失敗 (或不穩定) 後建置成功將會觸發寄送郵件，告訴大家危機已經解除。
3. 建置成功後如果發生建置不穩定也會觸發寄送郵件，昭告天下我們又倒退了一步。
4. 除非另外設定，不然每次不穩定的建置都會觸發寄送郵件，告訴大家狀況還沒解除。
```

所以基本上很合理, 那為甚麼又需要裝個 Extend 套件呢?

因為當有符合寄信條件的情況發生後, jenkins 就會用他的範本寄一樣的內容出去, 不管今天是 unstable 還是 failed 

>(信件範本檔位置請自行 google)

但是我們會希望今天 build 的結果不同的情況下, 能寄出不同內容的信, 而且是寄給不同的人, 那我們就要另外在裝這個套件了

  
#### 1. 安裝 Email Extension plugin

[ref https://wiki.jenkins-ci.org/display/JENKINS/Email-ext+plugin]

#### 2. SMTP 設定

其實跟原本的設定一樣, 但是他不會去吃原本你的 SMTP 設定, 所以這裡就在設定一次吧

#### 3. 信件內容設定

在剛剛 SMTP 設定的過程中會發現, 有其他的信件內容設定可以去輸入, 那這些就是剛剛講到的, 為什麼要另外裝這個套件的理由

![](/assets/xemail setting.PNG)

我們可以在這裡先設定好一些預設要寄出去的內容, 就不用在 job 的組態裡面去 key

> 這裡提供我的例子

首先要先將 ```Default Content Type``` 設為 ```HTML (text/html)``` 格式, 否則你的 html 語法寄出去會只有文字檔

![](/assets/content type.PNG)

```bash
<hr/>
Git commit: $GIT_COMMIT<br/><br/>
Git  branch: $GIT_BRANCH<br/><br/>
Git URL: $GIT_URL<br/><br/>
Status: $BUILD_STATUS<br/><br/>
Cause: ${CAUSE}<br/><br/>
Console output: <a href="${BUILD_URL}console">${BUILD_URL}console</a><br/><br/>
<hr/>
${JELLY_SCRIPT,template="html"}<br/>
<hr/>
```

> ```$GIT_COMMIT``` 等的環境變數為 Git plugin 提供的, 可以到他的 wiki 去看哪些可以使用, 不過我在使用過程中, 有些變數還是會沒有內容, 目前還不知道原因

> 以上的內容下面會在 show 出來

> 關於 ```${JELLY_SCRIPT,template="html"}``` 表示用 jelly script 去寫的網頁樣示, 不過我還沒研究, 暫時這樣 key 就能直接用他的模版了, 這邊表示將 changeset 的內容都 show 出來

> 實際會是這樣

![](/assets/changeset.PNG)

#### 4. job 中的信件內容設定

雖然剛剛已經有設定內容了, 或者剛剛都用預設的沒有改設定, job 組態頁面裡面還是有提供 user for job 去做信件內容的設定

一樣在建置後事件裡面去 ```Add post-build action``` 加入 ```Editable Email Notification```

會發現類似剛剛設定內容的頁面, 這裡就可以在設定一次這個 job 要寄出信件的預設內容以及收件者等

![](/assets/build xmail setting1.PNG)

那假設今天 fail 跟 unstable 要寄的內容跟收件人不同, 就點下面的 ```Advanced setting```可以透過不同的 trigger 來作針對性的修改

![](/assets/build xmail setting2.PNG)

![](/assets/xemail trigger.PNG)

我這裡的例子已經加入了 ```Ubstable (Test Failures)```  跟 ``` Failure - Any``` 兩個 trigger

> 在 ```Configure System``` 中 Default 的觸發設定就是 ```Failure - Any``` 這個條件了, 但那邊是給 global 使用, 這裡如果我們要針對 job 再做修改, 就要再加一次 ```Failure - Any``` 的情況了

而這裡有提供了各種的觸發條件, 可以依需求去選擇

![](/assets/add trigger.PNG)

這樣就可以對不同的清況寄的信件有所區別了

配合剛剛 ```Log parser console``` 的功能, 我們就可以將 warning 和 error 的信件分開處理

另外他已經有提供了一些收件者給我們去選擇

![](/assets/xemail send to.PNG)

> 關於各個表示, 可以點開問號會有說明

> _這個部分還沒有很多的使用測試, 所以還不確定實際上的信件會寄給誰_

而信件的內容這邊提供了我的例子

```bash
<h2>$PROJECT_NAME - Build # $BUILD_NUMBER</h2>
<hr/>
<h3>Warnings</h3>
<font color="   #FF9224">${BUILD_LOG_REGEX, regex="warning:", showTruncatedLines=false}</font><br/>
<br/>
See <a href="${BUILD_URL}parsed_console">${BUILD_URL}parsed_console</a>
$DEFAULT_CONTENT
```

> $BUILD_LOG_REGEX 這個變數提供我們從 Log 中用正則表示式來找出字串, 這樣我們就能直接找出重點寄信給收件人

> 這個變數的使用說明可以參考 http://siddesh-bg.blogspot.tw/2012/04/using-buildlogregex-in-jenkins-email.html

我們可以觀察到信件有兩種變數前綴, 以 ```Recipient List``` 為例子, 會有 ```$DEFAULT_RECIPIENTS``` 與 ```PROJECT_DEFAULT_RECIPIENTS```, 前者表示是由 ```Configure System``` 中所設定的參數, 後者表示是由 job 這邊所設定的參數

> 那關於信件的內容以及各欄位的說明, 除了他的套件官方頁面, 也可以到這裡看看中文的說明 http://www.cnblogs.com/zz0412/p/jenkins_jj_01.html

### 5. 看結果

因為可以使用 html 所以我們可以設計漂亮的信件內容, 剛剛收到信就如下圖

![](/assets/xmail reslut.PNG)

#### 還能直接看到 error 跟 warning 的內容, 真的是方便了許多!

> 因為我們剛剛有使用 $BUILD_LOG_REGEX