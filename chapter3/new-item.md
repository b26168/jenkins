新增一個 job
====

在 Jenkins 中, 每一個部屬的專案我們稱之為 Job 或是 Project, 在剛剛完成了 Jenkins 的安裝以及 git repository 的設定後, 我們就可以來嘗試新增我們的第一個 job 了.

當然你也可以沒有 git repository 就開始新增一個 job, 不過似乎沒有意義, 所以我們在新增 job 之前才會先將 git repo. 連結好在接著作下面的步驟

#### 1. 新增作業 job

在初始畫面的右邊選項選擇 ```New item```.

![](/assets/new item.PNG)

假設你又安裝其他的套件, 這一頁會跟下面畫面一樣很多 project 的樣板

這裡我們選擇 ```Freestyle project``` 就好了

然後 key 上 project name

> 建議不要有空格跟中文, 因為 project name 會做為這個 job 的 URL

![](/assets/new item2.PNG)

#### 2. 連結 git repository 設定

接著會看到 configure 的畫面如下

![](/assets/new item3.PNG)

上面的 tab 可以直接快速的跳到該主題區域, 或著直接網頁往下拉也能到達目的區域

我們在這裡的重點是設定 git repo.

所以直接到 ```Source Code Management``` 的區域點選 git

> 假設沒有安裝 git plugin 就不會看到拉!

![](/assets/new item4.PNG)

我們可以在 ```Repository URL``` 的地方 Key 上將 git repository 的 ssh URL 貼上

_可以點旁邊的問號參考他的格式 [https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin]_

基本上因為我們已經在前一章節設定好了 git 跟 ssh 的連結, 所以 ```Credentials``` 就不用特別設定了

然後選擇我們要 build 的 branch, 最後 Save 就 OK 了!