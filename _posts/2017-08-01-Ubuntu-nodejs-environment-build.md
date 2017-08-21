---
layout: post
title:  Ubuntu nvm搭建nodejs环境
date:   2017-08-01 23:36:00 +0800
categories: 环境搭建
tag: ubuntu
---

* content
{:toc}


## 前言

node是一个很受欢迎的语言，ubuntu也是linux下特别受欢迎的操作系统，故而记录下自己在ubuntu下搭建node环境的步骤。nvm是用来管理node的工具，十分方便，故采用nvm来下载安装node。   
注意ubuntu系统最好为14.04及以上，而此时系统的node环境干净，也就是系统并没有安装过node。这样的条件是最好不过。

## 使用nvm下载管理node环境 
 
1. 安装git 采用命令  ```sudo apt-get install git```  

2. 获取nvm  ```git clone https://github.com/creationix/nvm.git```  

3. 进入目录，安装  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```cd nvm/```  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```sh ./install.sh```  

4. 安装之后,输入nvm还是提示没有,这时候需要执行  ```source ./nvm.sh```  

5. 使用nvm安装管理nodejs：  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```nvm ls```  查看当前已经安装的node或者iojs版本  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```nvm ls-remote```  查看当前可以安装的node或者iojs版本  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```nvm install v6.11.2```  安装制定版本的nodejs  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```nvm use v6.11.2```  切换使用的nodejs版本  
我采用最后两行命令，下载安装node v6.11.2

6. 接下来需要使用```nvm alias default 6.11.2```将其设定为默认版本。如果关闭终端后node打不开，则是这条命令没有起作用。重新输入这条命令。  

7. 这样安装之后，使用sudo node会提示找不到node。使用下面方法解决：  
输入  ```whereis node|awk -F ' ' '{print $2}'```找到node安装路径，可能将$2改为$3或者$4等等，找到你的路径。    
然后输入下面命令将当前环境node链接到sudo环境(将$nodepath改为上面的结果)：  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```sudo ln -s $nodepath  /usr/bin/node```  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```sudo ln -s $nodepath  /usr/bin/nodejs```  
同理sudo npm提示找不到命令，也可以用这种方法，即使用命令 ```whereis npm|awk -F ' ' '{print $2}'```，然后输入```sudo ln -s $npmpath  /usr/bin/npm```，将$npmpath用第一条命令结果替换就行。  
8. 输入```npm -v```，```node -v ```，```nvm --version ```分别查看所装软件版本，至此ubuntu下node环境搭建完毕

## 后记

若是一次搭建不成功，则可以断掉链接再按此步骤重新来一遍，断掉链接方法如下：  
&nbsp;&nbsp;&nbsp;&nbsp;
```rm -rf   symbolic_name```  
比如按此教程，则为如下两句：  
&nbsp;&nbsp;&nbsp;&nbsp;
```rm -rf   /usr/bin/node```  
&nbsp;&nbsp;&nbsp;&nbsp;
```rm -rf   /usr/bin/nodejs```  
我后面在另外一台pc上又搭了一次，node是没问题，但是npm找不到了，然后重来了一次，就好了，估计是在某一步骤出了些差错。
