---
layout: post
title:  windows下，树莓派SD卡烧录系统并搭建
date:   2017-08-16 20:34:00 +0800
categories: 环境搭建
tag: Raspberry pi
---

* content
{:toc}


## 前言

很早的时候就弄到了一个3代树莓派，一直也没时间玩，现在正好趁着这个暑假玩玩。树莓派其实就相当于一个微型电脑，要玩树莓派，首先就得给它装一个系统。

## 所需工具  

1. 树莓派板子
2. SD卡
3. 读卡器  

建议分开购买树莓派各部件，而不是买套装，毕竟套装包括许多我们用不上的套件。另外买SD卡的时候，一般会附带读卡器，以及一个叫micro SD Adapter的东西：   
![sd-adapter](http://ouebtut1h.bkt.clouddn.com/sd-adapter.jpg)  
其实它相当于一个适配器的作用，可以将SD卡插入，拓展其大小。当然它还有一个很重要的作用，就是将SD卡的写保护去掉，即将Lock附近的按钮往下划。

## 步骤

1. 选择自己喜欢的[系统](https://www.raspberrypi.org/downloads/)，我选择的是UBUNTU MATE，点击图标，找到链接，下载镜像即可。  
2. 将SD卡插入读卡器后，将读卡器插入电脑。点击“我的电脑”查看是否多出来一个盘，否则就没有正常读入SD卡，可能读卡器或者SD卡有问题。  
3. 将镜像写入SD卡。这是需要相关的工具的，开始我下了一个叫ImageWriter的，但是打开之后才发现它不仅只识别.raw后缀的镜像，而且无法识别SD卡所在的盘。故而后来又下载了一个叫win32diskimager的软件，这次就可以正常操作了。点击Win32DiskImager.exe运行：  
![](http://ouebtut1h.bkt.clouddn.com/win32DiskImage.PNG)  
正常情况下，Device栏下会自动识别，如果没识别，可以自己点击下拉菜单进行选择。镜像文件也可以通过后面的蓝色图标进行选择，选好之后，点击Write即可写入。
4. 这样SD卡就写入了刚刚下载下来的镜像了。将SD卡插入树莓派板子，接着上电接入显示器就进入熟悉的linux系统安装的画面了。

## 一些问题

1. 在第3步写入镜像时，可能会报IO异常，无法写入的错误，这是因为SD卡开着写保护的原因，可以将SD卡插入适配器，滑下按钮。但是这样就得将整个大卡插入读卡器，配套的读卡器可能就不适用了。  
不过去掉写保护还有很多方法，直接参照[这里](http://jingyan.baidu.com/article/e75aca85b3ea38142fdac652.html)即可。我采用的是第三种方式。
2. 关于windows识别Linux文件系统的问题。对于写入镜像的SD卡，windows读取的可能只有boot引导部分的内容，我的为64MB，而我的SD卡可是有32GB的内存空间的！这是因为windows和Linux文件差异的缘故。  
你可以鼠标右键"我的电脑"->"管理"->"磁盘管理",就可以看到这个盘的大概分区了，不过并不能进行修改。

## 下一步工作  

1. 对树莓派SD卡进行扩容。由于SD卡刷入系统，默认使用的大小与刷入镜像大小相关，故大量空间未被使用，这个更改SD卡分区容量的教程也有很多，搜索"树莓派 SD卡 分区扩容"等关键词就有很多教程文档，大致就是在树莓派下使用fdisk工具进行扩容。  
由于初次碰到，走了许多弯路，不懂为什么会有很多空间剩余，而且windows只识别了引导部分的SD卡大小，所以在windows下使用了一个叫DiskGenius的工具，不断格式化和分区进行摸索，最终达到了利用fdisk一样的效果(本人SD卡为32G)：  
![](http://ouebtut1h.bkt.clouddn.com/df-h-.jpg)  
但是我还是推荐树莓派下使用fdisk工具的做法。  
当然最简单直白的方法是直接在树莓派下运行sudo raspi-config，然后选择里头的Expand FileSystem再重启即可。不同的系统这个顺序还不太一样，有可能藏在Advanced Options里头等等。  
2. Ubuntu Mate系统默认不打开SSH服务，所以得自己手动设置一下。参见[博文](http://yjgit.github.io/2017/08/18/raspberry-ssh-open/)。  
3. 可能树莓派系统时区和时间不对，确保树莓派连入网络，打开终端输入```sudo dpkg-reconfigure tzdata```，即可进行更改。  