Git plugin setting
====

為了讓 Jenkins 能夠使用 git, 所以這裡我們馬上來安裝第一個套件吧!

> 之後我們如果要安裝套件, 也是類似的步驟.

#### 1. 安裝套件

選擇 ```Manage Jenkins```

![](/assets/Manage Jenkins.PNG)

接著可以看到下面的畫面, 基本上就是所有 Jenkins 的設定都在這裡了

![](/assets/config page.PNG)

我們選擇 ```Manage Plugins```

![](/assets/plugin page.PNG)

上面會有 4 個 Tab, ```Updates```, ```Available```, ```Installed```, ```Advanced```.

我們點選 ```Available``` 會看到好多的 plugin, 聽說 Jenkins 有數以千計的 plugin

我想我們還是直接 key ```Filter``` 吧!

找到以後就勾選並安裝吧!

> 會有 ```Install without restart``` 跟 ```Download now and install after restart``` 的選項, 大部分情況下只要選 ```Install without restart``` 就安裝就好了

#### 2. 設定 git plugin

安裝完成後, 我們回到 ```Manage Jenkins``` 的畫面

選擇 ```Global Tool Configuration```

![](/assets/gitplugin setting.PNG)

將 ```Default``` 的 git executable 路徑設定到你本機的 git 執行檔位置就好了

這樣基本上就完成本章的 git 設定了

###_以上跟今後的設定請記得都要按 Save_