---
layout: post
title:  MySQL的简单使用
date:   2017-08-02 10:59:59 +0800
categories: 软件工具使用
tag: MySQL
---

* content
{:toc}


## 前言

MySQL是一个常见的关系型数据库管理系统，使用非常普遍，也很方便。常常搭建系统都会用到它，故在此记下一些常用的方法，以供参考，以后也不用到处查找资料。

## 简单的使用

1. 进入MySQL，输入：  
    &nbsp;&nbsp;&nbsp;&nbsp;
    ```mysql -u root -p;  //root用户```  
之后输入密码，看到 mysql>，即进入成功。

2. 数据库和表的创建、删除、查看操作   
```create database test;```  创建名为test的数据库  
```drop database test;```  删除名为test的数据库  
```create table test_table (Id Int, data VARCHAR(80));```  创建名为test_table的表  
```drop table test_table;```  删除名为test_table的表  
<br>
```show databases;``` 查看MySQL中数据库  
```use test(数据库名);```  使用名为test的数据库  
```show tables;```   查看所使用数据库下的所有表格  
```select * from test_table(表名);```  查看表test_table里的所有内容 

3. 表内容的插入、删除、更新操作，以test_table为例：     
插入数据  ```INSERT INTO test_table VALUES (值1, 值2,....)``` 
删除数据  ```DELETE FROM test_table WHERE 列名称 = 值```  
更新数据  ```UPDATE test_table SET 列名称 = 新值 WHERE 列名称 = 某值```     

4. 远程连接MySQL
在装有MySQL环境的PC里运行，```mysql -h xxx.xxx.xxx.xxx -P PORT -u USER -p```  
"-h" 远程MySQL主机地址  "-P" 远程MySQL主机开放端口  "-u" 远程MySQL主机用户名  
然后同上输入密码即可访问到远程MySQL。

## 注意
MySQL命令在结束时均需要加入;号。