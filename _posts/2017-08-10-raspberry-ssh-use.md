---
layout: post
title:  windows系统SSH连接树莓派
date:   2017-08-19 21:25:00 +0800
categories: 环境搭建
tag: Raspberry pi
---

* content
{:toc}


## 前言

刚刚给树莓派卸掉了Ubuntu Mate系统，又装上了官方推荐的Raspbian。像之前一样给SD卡扩了容，打开了SSH服务，不过相比于Ubuntu Mate系统，Raspbian初始的账号名和密码均为pi，需要自己更改一下，同样是运行```sudo raspi-config```即可进行更改。  
现在我们就可以愉快的使用ssh登入树莓派了，使用ssh有两种方法：  

## 方法一 

SSH远程登入，比较常用。  
1. 找到树莓派IP。第一次需要使用外接显示器，键盘，鼠标等，登入树莓派系统，在左上角选择联网的WIFI，并且连上网。然后打开终端，输入```ifconfig```：  
![](http://ouebtut1h.bkt.clouddn.com/wlan0-.jpg)  
图中标红的就是树莓派IP。  
2. windows主机下打开PUTTY软件(如果没有，自行下载):  
![](http://ouebtut1h.bkt.clouddn.com/putty.PNG)  
在上面的框里输入IP，在下面的框里输入一个有意义的名字，点击save(这样下次可以直接双击这个名字就能打开)，然后点击open，之后输入用户名和密码，即可登入树莓派了。  

## 方法二  

(**注意**：这个我在自己电脑上没有实验成功，但是用别人的电脑使用成功了，目前也不知道是什么原因，记在这里也就是当作一种trick)  
一根网线连接windows主机和树莓派，登入。不需要外接设备，树莓派也不用事先联网。  
1. 网线连接两者。并且将树梅派连接电源。  
2. windows下鼠标右键wifi图标，打开“网络与共享中心”，选择右边更改“适配器设置”。  
3. 右键你连网的wifi，选择属性。切换至共享，勾选第一个，在下面选择你要共享的网络，也就是树莓派连接的网络(这个你可以通过看刚才的页面，哪个网络无法识别就选哪个)。  
![](http://ouebtut1h.bkt.clouddn.com/share.PNG)  
点击确定即可。  
4. 打开windows的cmd命令行。输入```arp -a```:  
![](http://ouebtut1h.bkt.clouddn.com/arp-a.PNG)  
图中192.168.137.1下的第一行即为树莓派的IP，可能为静态的。之后就按方法一ssh进入即可。  

