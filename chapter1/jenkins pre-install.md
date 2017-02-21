安裝 Jenkins 的前置作業
====

首先我們先檢查看看我們的 Mac 中有沒有安裝 JAVA 跟 JDK, 因為 Jenkins 主要是 JAVA 開發的, 假設電腦中沒有的話, 裝完 Jenkins 後, 會無法連接到 Jenkins 的頁面, 等於是白裝了

然後 Jenkins 使用上建議是 JDK 1.7 以上的版本, 所以假設發現版本過低, 也是要再裝一次喔!


#### 如何檢查 Java 版本?

#####請開啟 Terminal 輸入以下指令

```bash
java -version
```

他可能就會出現以下的訊息

```bash
 java version "1.8.0\_121"

 Java\(TM\) SE Runtime Environment \(build 1.8.0\_121-b13\)

 Java HotSpot\(TM\) 64-Bit Server VM \(build 25.121-b13, mixed mode\)
```

代表你已經有安裝 JAVA 1.8.0_121 的版本 以及 Java SE Development Kit 1.8.0_121-b13 的版本了


#### 假如沒有的話, 作下面兩個步驟吧!

1. 安裝 Apple's Java

    http://support.apple.com/kb/DL1572

2. 安裝 Oracle Java 8

    http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

####裝完以後你還需要作環境變數的設定

```bash
vi ~/.bash_profile
```
增加 JAVA 的環境變數
```bash
export JAVA_HOME=$(/usr/libexec/java_home)
export PATH=$JAVA_HOME/bin:$PATH
```
可以用
```bash
echo $JAVA_HOME 
```
測試一下有沒有成功, 有訊息 show 出來就 OK 了!
    
<br/>
        
ref: https://wiki.jenkins-ci.org/display/JENKINS/Thanks+for+using+OSX+Installer
