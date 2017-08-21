---
layout: post
title:  树莓派 respbian系统搭建喜欢的nodejs环境
date:   2017-08-21 22:13:00 +0800
categories: 环境搭建
tag: Raspberry pi
---

* content
{:toc}


## 前言

respbian系统是官方推荐的树莓派系统，我的树莓派使用的就是这个系统，最近发现它自带的node环境版本太低，就想着安装一个更合适的node环境。

## 步骤 
 
1. 删除原有的node环境，使用下面两个命令：  
```sudo apt-get remove nodejs nodered```  
```sudo apt-get autoremove```  
2. 接下来使用nvm来安装管理node环境，参见[博文](http://yjgit.github.io/2017/08/21/respbian-system-nodejs-upto-newest/)。  
虽然博文名字为Ubuntu系统下用nvm下载管理node，但是同样使用于树莓派的respbian系统，毕竟linux核心都是一样的。

