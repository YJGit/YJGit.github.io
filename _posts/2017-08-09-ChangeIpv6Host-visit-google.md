---
layout: post
title:  windows改Hosts，通过ipv6访问google
date:   2017-08-09 10:34:59 +0800
categories: 环境搭建
tag: 翻墙
---

* content
{:toc}


## 前言

国内访问google的方式有很多，比如vpn和ss，不管自己搭建还是购买服务都可以。再比如一些专门的软件，像老牌的自由门等等。  
但是最近管理得比较严，很多服务都被封掉了，故而我最近又捣鼓了改hosts方法，通过ipv6访问google，这样是有一些限制的，只能访问国外提供ipv6服务，并且知道相关主机的hosts，才能得到相应的服务，不过幸好有人整理过一堆hosts，我觉得作为学术和一些基本的娱乐，改hosts方法已经足够了。  
**注：本人使用的是windows**  

## 具体方法

1. 确定本机能够访问ipv6，不能的话就需要自己设置，网上有许多教程，而且一般校园里连网线都能走ipv6，故不在此详述。怎样确定？有专门的测试平台，不过我忘了，我觉得直接访问一些ipv6资源也能确定你能不能上ipv6，比如[北邮人](http://bt.byr.cn/)。   
2. 上github搜索ipv6字样，就能找到ipv6-hosts这样的仓库，点击进入，下载其中的hosts文件。  
![github-hosts](http://ouebtut1h.bkt.clouddn.com/github-hosts.PNG)  
3. 找到本机的hosts文件，windows在C:\Windows\System32\drivers\etc目录。  
![windows-hosts](http://ouebtut1h.bkt.clouddn.com/windows_hosts.PNG)  
4. notepad++打开hosts文件，直接将下载下来的hosts文件粘贴到此文件末尾，保存。若是用notepad++打开，它会自动请求以管理员身份重新打开程序，点击允许即可，重新打开后，ctrl+s保存即可。其他文本编辑软件似乎不会自动请求，也就保存不了hosts文件，此时比较直接的方法就是先把windows下的hosts文件移到桌面，打开复制保存后再移回去。  
5. 最后，打开windows命令行，随便哪里都行，我一般喜欢在windows搜索栏直接打入cmd回车。输入  
&nbsp;&nbsp;&nbsp;&nbsp;
```ipconfig/flushdns```  
这样就可以打开Google Chrome，输入YouTube即可访问了。  
![youtube](http://ouebtut1h.bkt.clouddn.com/youtube.PNG)  

## 一些注意事项

首先一定要确认自己是否能上ipv6。  
其次推荐使用Google Chrome，体验更佳，当然火狐浏览器也行，其他浏览器未试验，觉得应该也可以。  
最后若是依然访问不了，可以选择重启一下试试。若是之前配过ss或是vpn什么的，记住要更改设置，此时Google Chrome优点就出来了，它会提示你进行更改。  
另外虽说是通过ipv6访问google，但是你最好打开ipv4上网，因为你访问国外一些网站的时候，可能会点到一些链接跳入国内，这时候就得通过ipv4访问了。  
