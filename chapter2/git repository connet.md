連結 git repository
====

#### 有使用過 github 或 bitbucket 的人, 應該都會有要設定 git 連結的經驗, 需要與本機的電腦作 SSH Key 的連結

#### 現在 Jenkins 就是我們當初使用 github 或 bitbucket 的電腦本機, 先將電腦連接到我們的遠端儲存裝置吧!

#### 1. 產生 SSH Key

先看看 ```~/.ssh``` 有沒有現有的 key, 也就是 ```id_rsa```, ```id_rsa.pub``` 兩個檔

有的話就不用產生了, 沒有的話
```bash
ssh-keygen -t rsa
```
_也有可能已經有 key, 但是名稱不是 id_rsa, id_rsa.pub, 如果要直接使用可以自己寫 config_

#### 2. 複製 public key 到 repository

將 ```id_rsa.pub``` 的內容複製到你的 git repo. (bitbucket, github ...等) 去 Add ssh key

網路上很多相關教學, 這裡就不贅述了.

#### 3. 加入 ssh host 到 known list

複製 repo. 的 ssh path, 例如 bitbucket 是 ```git@bitbucket.org```

然後下連接 ssh server 的指令
```bash
ssh git@bitbucket.org
```
會有一行問你 yes or no? 就 key yes 吧

接著看一下 ```./ssh``` 目錄下有沒有 ```known_hosts``` 檔, 並且看看內容有沒有 ```bitbucket.org```

有就完成了

> windows 的 key 需要複製到 C:\Windows\System32\config\systemprofile.ssh

<br/>

ref http://damien.co/development/how-to-install-jenkins-ci-on-a-mac-os-x-with-git-bitbucket-8072