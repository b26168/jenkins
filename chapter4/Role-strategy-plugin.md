Role strategy plugin
====

這裡要介紹的是關於使用者設定的套件, 他可以方便我們去分類不同的 user, 給予他們不同的使用權限

#### 1. 安裝 Role strategy plugin

[ref https://wiki.jenkins-ci.org/display/JENKINS/Role+Strategy+Plugin]

> 實際找到似乎也不是這個名稱

#### 2. 設定 Role strategy plugin

跟目前為止的其他套件相比, 比較特別

他除了不用在 ```Configure System``` 裡面去設定, 也不是到 job 的設定頁去設定

當我們進到 ```Manage Jenkins``` 的功能頁以後, 會發現一個新的功能選項 ```Manage an Assign Roles```

![](/assets/manage and assign roles.PNG)

點進去之後會看到這個畫面

![](/assets/manage role.PNG)

基本上我們使用到 ```Manage Roles``` 跟 ```Assign Roles``` 而已

![](/assets/manage role setting.PNG)

可以看到他能夠針對 Global, Project, Slave 三種層級去分類 Roles

假設是 ```Global roles``` 的設定, 他只有開放一個 ```Role to add``` 的功能, 除了預設有 ```admin``` 的 Role, 我們在這裡另外加上了 programmers, project leader, watcher

接著就針對權限內容一個一個勾選

假設是 ```Project roles```, ```Slave roles``` 的情況, 有多提供了 ```Pattern``` 去讓你做更細的分類

#### 3. 指派角色

_在指派角色之前, 系統資料庫要先有其他的 user 吧? 到 ```Manage Jenkins``` -> ```Manage Users``` 去新增吧_

剛剛在 ```Manage and Assign Roles``` 的頁面還有看到一個 ```Assign Roles``` 的選項, 在完成了 Roles 設定後, 我們還要把系統裡面的 user, 一個個的 assign 給他不同的角色

![](/assets/manage user.PNG)

這裡一樣分了三個層級分類, 不過參數內容是一樣的

就將 user 一個個手 key 進去

> 他沒有 auto. picker 的功能, 然後也不能修改, key 錯只能砍掉重加...

#### 4. 安全設定

權限這種東西, 就是為了系統以及資料的安全來設計的, 所以在一切都設定完後, 請到 ```Configure Global Security``` 中修改安全設定

![](/assets/configure global security.PNG)

> 最上面的 ```Enable security``` 要先勾選

看到 ```Authorization``` 區域會有一個 ```Role-Based Strategy```, 這是安裝完 role strategy plugin 才會有的選項

勾選他以後, 系統的權限就會 follow 我們剛剛的設定了

#### 最後可以用不同的使用者登入測試看看

> 還記得在 email extension plugin 裡面, 有一個可以設定信件收件人的設定
>
> 原本是想要讓他引用這邊的角色來傳送信件, 但目前還沒找到方法
>
> _Jenkins 有一個問題就在於, 不同的套件之間都是獨立的個體, 除非他們個別都有提供一些環境變數給外部使用, 不然都很難進行互動_
>
> 一個例子就是 log parser plugin 的 parse 規則是用一個檔案設定, 而會發現很多 plugin 也會有簡單的 parse 功能, 但是大家都是自己設定自己的, 增加很多麻煩
