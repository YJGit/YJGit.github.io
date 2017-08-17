---
layout: post
title:  树莓派，Ubuntu Mate系统打开SSH服务
date:   2017-08-18 00:19:00 +0800
categories: 环境搭建
tag: Raspberry pi
---

* content
{:toc}


## 前言

刚刚给树莓派装上了Ubuntu Mate系统，又给其分区进行扩容。现在就得为其打开SSH服务。  

## 步骤

1. 登入树莓派系统，打开终端，输入```ps -e |grep ssh```  
如果可以看到ssh-agent，说明Ubuntu缺省安装了openssh-client，可以在树莓派ssh登录其他系统；如果可以看到sshd，说明安装了openssh-server，可以从其他系统通过ssh登录到树莓派。当然这里就是看不到的：  
![](http://ouebtut1h.bkt.clouddn.com/ssh-agent-.jpg)  
2. 输入```sudo raspi-config``，输入密码，然后选择Interfacing Options选项，此时你就可以看到SSH服务了：  
![ssh-](http://ouebtut1h.bkt.clouddn.com/ssh-.jpg)  
回车进入，选择yes之后，系统会自动进行配置，之后选择ok，然后Finish即可。(按TAB键进行选择按钮)    
3. 再次输入```ps -e |grep ssh```，可看到出现了sshd，此时表示打开了ssh服务。  