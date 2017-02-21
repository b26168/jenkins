Log parser plugin
====

[ref https://wiki.jenkins-ci.org/display/JENKINS/Log+Parser+Plugin]

事實上, 我們只需要知道 build 完以後有多少 warning, error, 但是 console output 一大串還需要自己去找錯誤訊息在哪邊, 實在是有點 stupid.

這裡使用到了一個簡單的 plugin, 能夠直接 parse user 設定的正則式(regular expression)字串去 show 出 error, warning, info, ok, start 的訊息並且 show 出來

#### 1. 安裝 Log Parser Plugin

跟上面的套件安裝方式一樣, 不再解釋

#### 2. 設定 Parse 內容

首先要寫一個給 Log Parser 能夠看懂得設定檔, 放在本機端, 格式如下

> level regx

例如我這邊使用的, 我只需要 parse error 跟 warning 兩種
```bash
error /error\:/
warning /warning\:/
```

如果一個 level 會有不同的 parse 格式, 只要換行在寫另一個格式就好了

#### 3. Log Parser 設定

一樣進入 ```Configure System``` 的設定頁面到 ```Console Output Parsing``` 的區域

```Parsing Rules File``` 就是剛剛創的那個檔案, 把他的路徑餵給他, 那 ```Description``` 就是你可以看到你要選擇甚麼 rule 的選項名稱(等一下就會看到)

之後完成就 ```Save```

_剛剛第二步驟的檔案我取名為 ```LogParseRule```_

![](/assets/parse setting.PNG)

#### 4. job 設定

進到 job 的組態設定頁面, ```Post-build Actions``` 區塊, 因為 console output 是要 build 完才會產生的

那在這裡 ```Add post-build action``` 選擇 ```Console output (build log) parsing```

![](/assets/postbuildstep.PNG)

之後就會出現 log parsing 的設定區塊, 可以看到幾個選項

```Mark build Unstable on Warning``` 表示當你 parsing 到 warning 的時候, 將這個 build 視為 Unstable

```Mark build Failed on Error``` 表示 parsing 到 error 的時候, 視為 Failed (不過我不了解為什麼要多這一項, 因為本身有 error 的時候, 自然就是 build failed  的結果了)

```Show log parser graphs``` 勾選的話, job 的 status 會出現一張圖表, 橫軸是 build numbers, 縱軸就是 有幾個 error, warning 等等

接著就是 ```Use global rule```, 就可以看到剛剛設定的 Description 選項了

```Use project rule``` 當然也可以為這個 project 在自己寫一個 rule 檔來用, 他跟 ```Use global rule``` 是互斥的

最後設定完一樣要 ```Save```

![](/assets/build parse setting.PNG)

> 另外一件很重要的事情, 會有沒有做 parse 的情況發生
> 假設你上一次 build 跟這一次的內容完全一樣, 基本上他 build 不會去 parse 到任何東西
> 因為他並沒有整個清空再 build, 只是簡單的 rebuild 而已
> 所以他的 console output 就沒有出現 warning 或 error 一些 build 的過程中才會出現的內容
> 自然就 parse 不到資料了
> 通常 build 之前我們會先清空上一次的 build, 這個之後就會講到了

#### 5. 看結果

在都完成也 build 完後, 我們可以進入每一次的 build 頁面, 看到左邊欄位多了一個 ```Parsed Console Output``` 的選項

> 之後的一些套件安裝完, 可能也都會在頁面多些選項

![](/assets/parsed console output.PNG)

點進去以後, 會發現他已經將 warning 與 error 分類好並作連結了, 當你點選他就會自動跳到 parsed 到的那一行

![](/assets/parse reslut.PNG)

比看 Jenkins 原本的 ```Console output``` 方便多了