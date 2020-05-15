[TOC]



# Virtual-Machine-Exercises

~~# Mac-OS-Exercises~~

~~virtual machine practice.~~

~~**` Install macOS Catalina.app `**  from App Store.~~

~~**`VMware® Workstation 15 Pro 15.5.2 build-15785246`**~~

~~`2020-04-29 20:48:31`~~

~~mac 下载的 OS 安装包需要在 mac 环境下制作成镜像，硬盘安装镜像也好，U 盘镜像也好，在 win 环境下制作成镜像目前比较困难。再议，估计五一后了。~~

~~`2020-04-30 23:04:50`~~

drawback，drawback，老呼用他的双系统黑 apple 上的 finder 重做了 dmg 文件，然后 folloow https://blog.csdn.net/sunxiaoju/article/details/104584425 这个帖子做了 ISO 镜像，在 VMware 上一跑竟然成了。

记录下命令行代码以防删帖

```
先把 apple store 下载的原版安装包文件放在桌面

mkdir -p /Users/darktimer/ISO/Volumes
mkdir -p /Users/darktimer/ISO/tmp
这是在用户名下创建两个目录

hdiutil attach /Users/darktimer/Desktop/Install\macOS\Catalina.app/Contents/SharedSupport/InstallESD.dmg -noverify -nobrowse -mountpoint/Users/darktimer/ISO/Volumes/install_app
具体不知道干嘛的 可能是给 dmg 做个链接

hdiutil create -o /Users/darktimer/ISO/tmp/Catalina.cdr -size 7800m -layout SPUD -fs HFS+J
创建 dmg 镜像

hdiutil attach /Users/darktimer/ISO/tmp/Catalina.cdr.dmg -noverify -nobrowse -mountpoint /Users/darktimer/ISO/Volumes/install_build
将 dmg 和 install_build 目录链接起来

asr restore -source/Users/darktimer/Desktop/Install\macOS\Catalina.app/Contents/SharedSupport/BaseSystem.dmg -target /Users/darktimer/ISO/Volumes/install_build -noprompt -noverify -erase
具体不知道干嘛的 可能是重编码了 dmg 文件

mkdir -p /Users/darktimer/ISO/Volumes/OS\ X\ Base\ System/System/Installation/
新建一个目录

cp -rp Users/darktimer/ISO/Volumes/install_app/Packages /Users/darktimer/ISO/Volumes/OS\ X\ Base\ System/System/Installation/
将 packages 拷贝到新目录

cp -rp /Users/darktimer/Desktop/Install\ macOS\ Catalina.app/Contents/SharedSupport/BaseSystem.chunklist /Users/darktimer/ISO/Volumes/OS\ X\ Base\ System/BaseSystem.chunklist
将BaseSystem.chunklist拷贝到/Users/sunxiaoju/sunxj/ISO/Volumes/OS\ X\ Base\ System目录，此目录在上一个mkdir已经创建过了

cp -rp /Users/darktimer/Desktop/Install\ macOS\ Catalina.app/Contents/SharedSupport/BaseSystem.dmg /Users/darktimer/ISO/Volumes/OS\ X\ Base\ System/
将BaseSystem.dmg 拷贝到/Users/sunxiaoju/sunxj/ISO/Volumes/OS\ X\ Base\ System目录中

hdiutil detach /Users/darktimer/ISO/Volumes/install_app
卸载install_app

hdiutil convert /Users/darktimer/ISO/tmp/Catalina.cdr.dmg -format UDTO -o /Users/darktimer/ISO/tmp/Catalina.iso
如果桌面上显示了Catalina镜像内容，请推出，否则无法将dmg转换成iso，会提示资源暂时不可用

然后生成的 iso 就可以用了。
```

在重装 OS 时提示需要互联网连接，重设了 VMware 的虚拟网络设置，选择 NAT ， VMnet8 的默认网关一定要写（还是学的不精啊，网关的概念现在还模糊）。

`2020-05-04 21:18:37`

终于成功了，好卡....还是白苹果好哇。

`2020-05-04 21:55:22`

# Linux Exercises

转战 Linux ，不玩 Mac 了。本质一样。项目就更名虚拟机联系吧，以后扩充方便管理。

`2020-05-04 18:15:03` 

------

## 2020-05-15 22:23:23

停滞了 N 天后，因为没有一本合适的入门书籍或者网站符合我的口味，Linux 和 macOS 都没怎么动，今天偶然从 良许Linux 公众号的推送上下载了 《Linux就该这样学》 这本电子书，初读感觉还行，准备接着开始看了。

话说，看来，开源这个概念，搞 Linux 的好像是最为引以为豪的一个群体。

我又犯了老毛病，老是想知道看的这本工具书在读者中是什么评价，意图读到最令大众满意评价最好的书，事实上这是不可能的。最起码看到第 1 章之前，作者写的话我都很认同没有感觉什么洗脑或者强加的意思，所以继续看就好了，至于鸟哥的私房菜什么的，先入了门再说。

------