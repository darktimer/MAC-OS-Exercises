[TOC]



## RPM 红帽软件管理器

功能相当于 WIN 里的控制面板，会建立统一的数据库文件，记录详细的软件信息，并且能自动分析软件之间的依赖关系。有一些常用命令，混脸熟。

## Yum 软件仓库

软件之间复杂的依赖关系使得在 linux 上安装装软件十分复杂，Yum 软件仓库就是用来降低软件安装复杂度的技术，它可以根据用户的需求，分析出需要的软件包和其依赖关系，然后从 Yum 服务器下载软件包并安装。Yum 中的 RPM 软件可以是红帽官方、第三方、甚至是自己编写。有一些常用指令，混脸熟。

## systemd 初始化进程

这个进程据说是替换了 redhat 之前版本的初始化进程，然后接管了很多诸如挂载文件系统、交换分区、启动各类进程服务等等初始化工作，还用的是并发启动机制，速度快的飞起。每一项任务进程都可以看做是一个单元，有不同的 target 类型来区别运行的功能。

## Shell 强大好用

Shell 名义是命令行工具，实际上就是充当人与内核的翻译官，通过命令调用相应服务。红帽的默认命令终端是 Bash（BShell）解释器，主要有四个特点：上下键调取之前的命令、Tab 键补全命令、批处理脚本、环境变量。

## 执行查看帮助命令

Linux 命令格式： 命令名称 命令参数 命令对象

**命令对象**：要处理的各种对象。

**命令参数**：长格式前缀 `--完整命令名称` ，短格式前缀 `-单个字母缩写` 。

第一个命令： **man man** 。打开了在线的参考手册。

```
[root@linuxprobe Desktop]# man man
```

## 常用系统工作命令

### echo

格式： echo 字符串 / $变量

作用：这个学 java 时见过，好像就是重复的意思，目前不太知道什么情况下会用到。

```
[root@linuxprobe Desktop]# echo Linuxprobe.com
Linuxprobe.com
[root@linuxprobe Desktop]# echo $SHELL
/bin/bash
```

### dat

格式： date 选项 +指定格式

作用：显示、设置系统时间或日期。

```
[root@linuxprobe Desktop]# date		显示系统时间
Sun May 17 10:44:58 CST 2020
[root@linuxprobe Desktop]# date "+%Y-%m-%d %H:%M:%S		以年月日时分秒显示时间
2020-05-17 10:47:30
[root@linuxprobe Desktop]# date -s "20200517 10:53:10"		设置系统时间
Sun May 17 10:53:10 CST 2020
[root@linuxprobe Desktop]# date		显示系统时间
Sun May 17 10:53:14 CST 2020
[root@linuxprobe Desktop]# date "+%j"		显示当天是当年第几天
138
```

### reboot

格式： reboot

作用：重启系统。

```
[root@linuxprobe Desktop]# reboot
```

据说这种涉及到硬件资源管理权限的命令只能用 root 管理员执行，但用 linuxprobe 用户也可以，看来 linuxprobe 也有 root 权限。

```
[linuxprobe@linuxprobe Desktop]$ reboot
```

为方便还是使用 root 吧。

### poweroff

格式： poweroff

作用：关闭系统。

```
[root@linuxprobe Desktop]# poweroff
```

### wget

格式： wget 参数 下载地址

作用：在终端中下载网络文件。

 