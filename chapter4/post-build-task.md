Post build task
====

為了上一章節使用 Workspace cleanup plugin 失敗的結果, 這裡又找到了另一個套件拉!

還記得我們在 build xcode 的時候是用 shell script 去達到目的的嗎?

這時候我就想

> 為什麼 build 可以打指令去執行, 我 build 完之後就不行呢???

於是就找到這個 plugin 拉!!

> 為什麼他的名稱後面沒接 plugin ???

既然我沒辦法用套件砍掉 folder, 那我直接在 build 完後下指令砍掉他總行了吧!

#### 1. 安裝 post build task

[ref https://wiki.jenkins-ci.org/display/JENKINS/Post+build+task]

> 有時候會發現他的名稱跟實際上在 Jenkins 找到的名稱不同
>
> 只要你發現點進去的 wiki 是對的就好了, Jenkins 很多套件更新後都可能不會更新官方網站的內容
>
> 大概因為工程師都懶得寫文件吧...

> 有時候也會發現套件名稱或是 library 檔案會有 ```hudson``` 這個詞, 其實是 Jenkins 的舊名, 有興趣的人可以自行去 google Jenkins 的歷史瞜

#### 2. 設定 post build task

他跟 workspace cleanup plugin 一樣, 直接進到 job 的組態設定頁面去設定就好了

![](/assets/post build task.PNG)

他有一些參數可以設定, 沒有仔細看 wiki 的教學內容, 但是似乎也是能夠針對不同的情況或 parse 不同內容執行不同的指令任務

但是這裡我們只是在 build 完後要砍掉 folder 而已

就直接 key 上 ```rm``` 指令吧

```bash
sudo rm -r $WORKSPACE
```

> $WORKSPACE 會自動取代成本機的 workspace folder

#### 3. 看結果

這裡就不看 folder 裡面的空氣了...

我們來看一下 console output 吧!

![](/assets/post build task log.PNG)

就能看到他實際上執行的指令是

```bash
+ sudo rm -r /Users/Shared/Jenkins/Home/workspace/obj-c-build-test
```

_不相信有沒有砍掉也可以真的到 folder 底下去看瞜_

#### 當然這個套件的功能不只這樣啦~ 有更多需要在 build 完做的事情也是可以使用他, 畢竟他是能直接執行 shell script 的

#### 要不是 workspace cleanup plugin 似乎有 bug, 殺雞焉用牛刀呢?