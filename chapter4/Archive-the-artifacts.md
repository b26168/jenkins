Archive the artifacts
====

在前面的功能有提到, 因為不想讓 code 被看到或者為了每次能正確的 parse console output 的內容, 亦或者其他原因

我們必須要在 build 之前或之後將 workspace 整個砍掉, 但是這樣不就連 build 完的成品也砍了嗎???

所以我們必須要在 build 完以後, 砍檔之前把成品取出來, 這樣就能留下成品了

> 其實 post build task 應該可以達成這樣的事情, 但是我還沒嘗試過

jenkins 提供了一個功能來達成這件事情, 不用大家煩惱

#### 1. 設定 Archive the artifacts

> 這次不用再安裝套件了

我們到 job 的組態設定頁面, ```Post-build Action``` 中能看到 ```Archive the artifacts``` 的 step 可以加入

加入以後就像這樣

![](/assets/archive the artifacts.PNG)

這裡透過設定 ```File to archive``` 來決定哪些檔案要被封裝為成品

我們這裡將整個 build 完的 Release folder 內容都留下

```bash
build/Release/
```

> 這邊是使用 ant 的語法, 點開問號他會叫你去參考這個網站
>
> http://ant.apache.org/manual/Types/fileset.html
>
> 底下會有一些 examples 教你設定你個 fileset

當然他也有ㄧ堆參數提供設定

![](/assets/archive the artifacts setting.PNG)

可以設定要排除哪些檔案, 或是當 build 成功時在封裝成品等等

#### 2. 看結果

build 完以後我們可以看到 job 的狀態頁會有 ```Last Successful Artifacts``` 的區域

![](/assets/artifacts.PNG)

那我們可以點 ```Last Successful Artifacts``` 連結進入

![](/assets/artifacts2.PNG)

直接點擊檔案就會下載, 想整個抓下來可以直接點 ```(all files in zip)```

#### 這樣就能把 build 砍掉只留下想留的東西了!

> 基本上他會存在本機的資料夾中
```bash
~/Home/jobs/
```

