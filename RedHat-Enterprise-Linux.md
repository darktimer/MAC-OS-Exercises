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

 这个如果没有经验的话就先了解一下就好，后边了解了 Linux 系统的配置管理方法和网卡的配置方法后再操作。

### ps

格式： ps 参数

作用：查看系统中的进程状态。

合理管理系统正在运行的进程有助于优化系统性能。 Linux 中常见 5 中进程状态：运行、中断、不可中断、僵死、停止。

R 运行：进程正在运行或者在运行队列中等待。

S 中断：进程正在休眠中，当某个条件满足后，或者，收到某个信号后，就终止休眠状态。

D 不可中断：进程不响应系统信号，用 kill 命令也不能中断。

Z 僵死：进程已经终止，但其描述还在，直到父进程调用 wait4() 系统函数后将进程释放。

T 停止：进程收到停止信号后停止运行。

```
[root@linuxprobe Desktop]# ps -a  显示所有用户的所有进程
   PID TTY          TIME CMD
  5482 pts/0    00:00:00 ps
[root@linuxprobe Desktop]# ps -u	用户及详细信息
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root       3740  0.3  3.8 293916 71208 tty1     Ssl+ 09:50   0:18 /usr/bin/Xorg :0 -background none -verbose -auth /run/gdm/auth-for-gdm-3EXbTz/database -seat seat0 -nolisten tcp vt1
root       4384  0.0  0.1 116260  2908 pts/0    Ss   09:50   0:00 /bin/bash
root       5486  0.0  0.0 123356  1376 pts/0    R+   11:23   0:00 ps -u
[root@linuxprobe Desktop]# ps -x	显示没有控制终端的进程
   PID TTY      STAT   TIME COMMAND
     1 ?        Ss     0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 23
     2 ?        S      0:00 [kthreadd]
     3 ?        S      0:00 [ksoftirqd/0]
     5 ?        S<     0:00 [kworker/0:0H]
     7 ?        S      0:00 [migration/0]
     8 ?        S      0:00 [rcu_bh]
     9 ?        S      0:00 [rcuob/0]
```

ps aux 命令会列出所有进程状态。

```
[root@linuxprobe Desktop]# ps aux	列出所有进程状态
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root          1  0.0  0.4  53676  7628 ?        Ss   09:49   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize 23
root          2  0.0  0.0      0     0 ?        S    09:49   0:00 [kthreadd]
root          3  0.0  0.0      0     0 ?        S    09:49   0:00 [ksoftirqd/0]
root          5  0.0  0.0      0     0 ?        S<   09:49   0:00 [kworker/0:0H]
root          7  0.0  0.0      0     0 ?        S    09:49   0:00 [migration/0]
root          8  0.0  0.0      0     0 ?        S    09:49   0:00 [rcu_bh]
root          9  0.0  0.0      0     0 ?        S    09:49   0:00 [rcuob/0]
```

USER ：进程所有者。

PID ：进程 ID。

%CPU ：CPU 占用率。

%MEM ：内存占用率。

VSZ ：虚拟内存使用量 KB。

RSS ：固定内存占用量 KB。

TTY ：所在终端。

STAT ：进程状态。

START ：被启动时间。

TIME ：实际使用 CPU 时间。

COMMAND ：命令名称与参数。

Linux 系统中的命令还记得吗，有长格式也有短格式，两个长格式的命令不能合并，长格式和短格式之间也不能合并，但两个短格式之间可以合并，合并之后可以只保留一个 - 符号，而且是可以省略的，所以会出现 ps aux 这样的命令格式。

### top

格式： top 

作用：动态监视进程活动与系统负载信息。

功能非常强大，动态的观看系统运维状态，是强化版的 windows 任务管理器。

```
[root@linuxprobe Desktop]# top

top - 16:13:12 up  6:23,  2 users,  load average: 0.12, 0.11, 0.08
Tasks: 520 total,   1 running, 519 sleeping,   0 stopped,   0 zombie
%Cpu(s):  4.4 us,  0.8 sy,  0.0 ni, 94.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem:   1870784 total,  1296248 used,   574536 free,      136 buffers
KiB Swap:  2097148 total,        0 used,  2097148 free.   292900 cached Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
  4125 root      20   0 2320892 535128  39088 S  40.2 28.6  11:19.43 gnome-shell 
  3740 root      20   0  293916  70928   7616 S   8.3  3.8   0:44.75 Xorg
  8348 root      20   0  622512  22008  12696 S   3.7  1.2   0:00.59 gnome-terminal-
   142 root      20   0       0      0      0 S   0.3  0.0   0:01.24 rcuos/4
  1109 root      20   0    4304    580    488 S   0.3  0.0   0:01.82 rngd
     1 root      20   0   53676   7632   2544 S   0.0  0.4   0:02.77 systemd
```

第一行：系统时间、运行时间、登录终端数量、系统负载（三个值分别是 1 分钟、5 分钟、15 分钟内的平均值，数值越小负载越低）。

第二行：进程总数、运行中进程数、睡眠中进程数、停止的进程数、僵死的进程数。

第三行：（本行数据均以 cpu 运行占比数据表示）用户占用资源百分比、系统内核占用资源百分比、改变过优先级的进程资源百分比、空闲的资源百分比等。

第四行：物理内存总量、内存使用量、内存空闲量、作为内核缓存的内存量。

第五行：虚拟内存总量、虚拟内存使用量、虚拟内存空闲量、已被提前加载的内存量。

### pidof

格式：pidof 参数 服务名称

作用：查询指定服务进程的 PID 值。

每个进程的 PID 是唯一的，可以唯一表示进程。