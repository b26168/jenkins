Build now
====

完成 job 的 Configure 後, 就能進行 job 的建置了

#### 1. Build

在完成了 ```Configure``` 後, 就會看到下面的畫面, 並且按下 ```Build Now```, 就會看到 ```Build History``` 有一個建置正在 run 的示意圖

![](/assets/initbuild.PNG)

> 在 Jenkins 中, Build 成功是藍色的, 失敗是紅色的, 還有一個 unstable 的狀態則是黃色的

![](/assets/build status.PNG)

#### 2. 查看建置的 Log

我們可以點選 Build 的編號, 進到下面這個畫面

> 剛剛的 build 完成且成功了, 所以顯示藍色的

![](/assets/build page.PNG)

我們可以點選 ```Console Output``` 看到剛剛的建置過程

![](/assets/buildlog.PNG)

可以看到系統自動幫你下了 git 的指令把 code clone 了下來, 因為這裡沒有在作其他事情了, 所以就算成功完成了建置!

#### 當我們新增了一個  job 時, 可以在首頁點選  ```My View``` 來觀看目前有哪些  job

![](/assets/my view.PNG)

![](/assets/my view list.PNG)

> 第一列是 ```S```, 代表 Status, 表示最後一次的 build status

> 第二列的 ```W``` 則是表示 Weather, jenkins 將 job 的 _最後五次 build status_ 統計成功機率, 分別將 0%, 20%, 40%, 60%, 80%, 100% 以不同的天氣圖表示

> 晴天 100%, 晴時多雲 80%, 陰天為 60%, 雨天 40%, 打雷 20% 跟 0%

![](/assets/sunny.PNG) ![](/assets/sunny when cloudy.PNG) ![](/assets/cloudy.PNG) ![](/assets/rain.PNG) ![](/assets/thunder.PNG)

> 接下來的欄位分別就是最後一次 build 成功與失敗的編號以及花多少時間

> 按下最後一列的時鐘圖示, 就會開始 ```Build Now```