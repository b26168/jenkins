開始 Jenkins 設定
====

#### 基本上到這裡會發現 Mac 的 User 多了一個 Jenkins 的使用者, 在所以事情開始之前, 先用 Jenkins 使用者登入你的 Mac 吧!

1. 設定 Jenkins 使用者的密碼
    
    首先當然要先設定一下這個 User 的密碼, 下面的指令能夠快速的初始他的密碼, 不用通過重重的 GUI 介面
    
    ```bash
    sudo passwd jenkins
    ```
    
2. 切換使用者到 Jenkins

    接下來的事情都在這個 User 上來操作了