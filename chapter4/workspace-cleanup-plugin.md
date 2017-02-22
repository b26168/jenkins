Workspace cleanup plugin
====

在 ```Log parser plugin``` 的章節提到, 假設上一次的 build 沒有清掉, 他可能因為是 rebuild 而沒有產生新的錯誤訊息, 導致無法正確的 parse 到有錯誤

所以這裡就介紹一個簡單能夠在 build 之前或是之後能夠砍掉整個 workspace folder 的套件

#### 1. 安裝 Workspace cleanup plugin

[ref https://wiki.jenkins-ci.org/display/JENKINS/Workspace+Cleanup+Plugin]

> ... 今後第一步是不是能省略不寫了??-.-

#### 2. 設定 cleanup

這個套件跟之前不一樣的地方在於, 他不用在進 ```Configure System``` 去設定一些參數了

直接進到 job 的組態設定頁面吧! 可以看到兩個地方的改變

在 ```Build Environment``` 的區域多了一個選項

> 我們超少來到這個區域做設定的...

![](/assets/cleanup before.PNG)

基本上這個地方打勾, 就會在每次 build 之前把 workspace 砍掉了

那下面的一些參數是讓 user 可以去排除一些檔案, 可能會有想留下的檔案, 相關設定就可以到他的官方網站去查看怎麼使用了

然後在 ```Post-build Actions``` 區域也有多了一個新的 Step

![](/assets/cleanup after.PNG)

在這裡只要 Add 了這個 action, 他 ```Clean when status is``` 預設就是全部的 status 都會在 build 之後砍掉啦~

#### 3. 看結果

_資料夾砍掉了是要看空氣嗎..._

我們可以從 job 的選項中選擇 ```workspace```

![](/assets/no workspace.PNG)

因為都沒檔案了, 所以點進來就甚麼都沒有了

> 假設你沒有要砍 build, 平常這裡是可以進來直接看到整個 project 的, 包含你的 code, 就是你整個 git repository 的內容拉~ 就像下面的圖一樣

![](/assets/workspace.PNG)

#### But, 九把刀小說最厲害的就是這個 But

#### 假設我們今天是 build xcode project

我們實際到本機 ```workspace``` 的目錄去看看

> 目錄在 ```~/Home/workspace/```

![](/assets/cleanup folder.PNG)

竟然會有一個檔名很奇怪的 folder!!!

其實 ```workspace``` 這個 folder 就是平常放 job workspace 的地方, 通常就是 job 的名稱當 folder 的名稱

> 這裡的 job name 是 ```obj-c-test```

但是發現這個目錄名稱是 ```job name_ws-cleanup_timestamp```, 而不是 ```job name```

事實上, workspace cleanup plugin 在幫我們清掉 workspace 的時候, 會先將 folder rename 為現在看到的這串名稱

等完成某些動作後再刪除

> 不知道是在哪個動作之後, 而導致他無法刪除

這裡也嘗試了 C# 的 project, 卻可以正常的刪除 folder, 所以在這裡我並不清楚是否是 xcodebuild 所造成的

不過總不能讓這些 folder 就這樣一直留著吧... 不然就是每隔一段時間來本機端砍砍檔案, 也太累人了!!

所以這裡只好又找了另一個套件來使用了, 將在下回介紹!