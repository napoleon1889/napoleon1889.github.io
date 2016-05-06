---
layout: post
title: 使用yum方式在centos6.5安装MySql最新版本
category: 数据库
tags: Linux MySQL
keywords: 
description: 
---

[toc]

#1安装MySql
##1.1下载MySql的yum仓库文件
选择适合你linux系统版本的仓库文件
[下载地址](http://dev.mysql.com/downloads/repo/yum/)
##1.2本地安装yum仓库
会下载一些依赖

```shell
#使用root权限，切换到yum仓库文件所在位置
yum localinstall mysql-community-release-el6-8.noarch.rpm
```

##1.3安装MySql服务

```shell
yum install mysql-community-server
```

#2初始化MySql
##2.1启动mysql服务
```shell
service mysqld start
#会出现以下结果
Initializing MySQL database:                               [  OK  ]
Installing validate password plugin:                       [  OK  ]
Starting mysqld:                                           [  OK  ]
```
##2.2修改密码
此时登录mysql是无法登录的需要修改密码
```shell
#停止mysql服务
service mysqld stop
#使用安全模式跳过密码验证
mysqld_safe --skip-grant-tables &
#新开一个shell
mysql -u root -p
#如果要求输入密码直接回车
#登录mysql
mysql> use mysql
mysql>update user set authentication_string=password('123456') where user='root';
mysql>flush privileges;
mysql>exit;
```
然后ctrl+c终止安全模式，正常启动mysql并使用修改的密码登录

#参考来源
http://blog.csdn.net/horace20/article/details/26516689
http://stackoverflow.com/questions/30692812/mysql-user-db-does-not-have-password-columns-installing-mysql-on-osx