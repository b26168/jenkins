開始安裝 Jenkins
====

#### 1. 下載安裝檔
    
我們可以到下面的連結到他的官方網站

https://jenkins.io/
    
![](/assets/jenkins download.PNG)

#### 2. 安裝 Jenkins
    
直接安裝包抓完就下一步一直按就裝好了

裝完後會自動開啟瀏覽器並連接到 localhost:8080

_如果這一步有問題，可能是沒有裝好 jdk_

接著我們會看到這個畫面
    
![](/assets/jenkins initpassword.PNG)
    
他告訴我們可以到
    
> /Users/Shared/Jenkins/Home/secrets/initialAdminPassword
    
這個連結去找初始的管理者密碼

_但是會發現目前的 user 無法進入到 secrets 這個目錄下, 所以直接複製路徑用 cat 指令吧_

```bash
sudo cat /Users/Shared/Jenkins/Home/secrets/initialAdminPassword
```

複製這串密碼貼上 "Continue"

#### 3. 設定管理者帳戶

我們可以趕快創一個新的管理者, 就不用每次都要用那串奇怪的密碼登入

#### 4. 選擇要安裝的套件

![](/assets/jenkins initplugin.PNG)

可以先不用裝任何套件, 其實右上角有 [X] 能按, 因為這些套件隨時都可以安裝或解安裝
  
現在想安裝的話, 選右邊比較快, 時間很多就選左邊吧

_有人選左邊, 好像就卡住了..._

#### 5. 安裝完成

就能看到初始畫面了

![](/assets/jenkins initpage.PNG)
