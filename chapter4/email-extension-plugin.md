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

#### 4. job 中的信件內容設定

雖然剛剛已經有設定內容了, 或者剛剛都用預設的沒有改設定, job 組態頁面裡面還是有提供 user for job 去做信件內容的設定

一樣在建置後事件裡面去 ```Add post-build action``` 加入 ```Editable Email Notification```

會發現類似剛剛設定內容的頁面, 這裡就可以在設定一次這個 job 要寄出信件的預設內容以及收件者等

![](/assets/build xmail setting1.PNG)

那假設今天 fail 跟 unstable 要寄的內容跟收件人不同, 就點下面的 ```Advanced setting```可以透過不同的 trigger 來作針對性的修改

![](/assets/build xmail setting2.PNG)

這樣就可以有所區別了

配合剛剛 ```Log parser console``` 的功能, 我們就可以將 warning 和 error 的信件分開處理

> 那關於信件的內容以及各欄位的說明, 除了他的套件官方頁面, 也可以到這裡看看中文的說明
> http://www.cnblogs.com/zz0412/p/jenkins_jj_01.html

### 5. 看結果

因為可以使用 html 所以我們可以設計漂亮的信件內容, 剛剛收到信就如下圖

![](/assets/xmail reslut.PNG)

#### 還能直接看到 error 跟 warning 的內容, 真的是方便了許多!