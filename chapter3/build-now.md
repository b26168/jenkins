Build now
====

完成 job 的 Configure 後, 就能進行 job 的建置了

#### 1. Build

在完成了 ```Configure``` 後, 就會看到下面的畫面, 並且按下 ```Build Now```, 就會看到 ```Build History``` 有一個建置正在 run 的示意圖

![](/assets/initbuild.PNG)

> 在 Jenkins 中, Build 成功是藍色的, 失敗是紅色的, 還有一個 unstable 的狀態則是黃色的

#### 2. 查看建置的 Log

我們可以點選 Build 的編號, 進到下面這個畫面

> 剛剛的 build 完成且成功了, 所以顯示藍色的

![](/assets/build page.PNG)

我們可以點選 ```Console Output``` 看到剛剛的建置過程

![](/assets/buildlog.PNG)

可以看到系統自動幫你下了 git 的指令把 code clone 了下來, 因為這裡沒有在作其他事情了, 所以就算成功完成了建置!