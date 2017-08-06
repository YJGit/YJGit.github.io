---
layout: post
title:  MySQL的表结构和数据的导入/导出
date:   2017-08-02 10:59:59 +0800
categories: 软件工具使用
tag: MySQL
---

* content
{:toc}


## 前言

本来以为MySQL表结构和数据的导入导出需要什么图形化工具，后来查了下资料，发现用两个命令就可以轻松搞定，故记录下来。  
这两个命令分别是mysqldump和source，使用也很简单，而且不需要另外安装，装好mysql就有了。

## 导出

使用的是mysqldump工具，命令行直接输入，就有使用帮助。常用的用法如下：  
1. 导出hostname的主机中的名为dbname的数据库的表结构到db.sql中  
&nbsp;&nbsp;&nbsp;&nbsp; 
```mysqldump -h hostname -u user -p -d dbname > db.sql```  
若是本地数据库，只可以省掉-h选项，以下均以**localhost**为例。  
2. 导出名为dbname的数据库中表名为test的表结构到db.sql中  
&nbsp;&nbsp;&nbsp;&nbsp; 
```mysqldump(mysql自带) -u user -p -d dbname test > db.sql```  
3. 导出名为dbname的数据库的表结构以及表数据到db.sql中  
&nbsp;&nbsp;&nbsp;&nbsp; 
```mysqldump -h hostname -u user -p dbname > db.sql```  
即**去除-d选项**  
4. 导出名为dbname的数据库中表名为test的表结构和数据到db.sql中  
&nbsp;&nbsp;&nbsp;&nbsp; 
```mysqldump(mysql自带) -u user -p dbname test > db.sql```  
即**去除-d选项**


## 导入

常用source命令。用法如下：  
1. 输入```mysql -u user -p ```，进入MySQL控制台  
2. 选择数据库，例如选择名为test的数据库:  
mysql> ```use test;```  
3. 使用source命令，后接脚本名，比如上面的db.sql:  
mysql> ```source db.sql;```  
注意，须在**脚本目录**下进入mysql，负责会找不到脚本