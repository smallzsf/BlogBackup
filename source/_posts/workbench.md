---
title: workbench 数据库管理工具
date: 2020-11-14 10:26:08
tags:
- 数据库
---

### 数据库连接方式

#### 数据库通过ssh密码连接方式

![图一](../workbench/ssh_conn_passwork.png)

- ***Connection Name*** : 
    表示本地查看的名字表示
- ***Connection Method*** :
    表示链接方式 在这里采用选择ssh 链接
- ***SSH Hostname*** : 
    表示链接的数据库所在的服务器地址，如果是本地就是127.0.0.1，``22`` 表示ssh 配置的端口号，默认22
- ***SSH Username 和 SSH Password***
    表示是ssh 登录的用户名和密码，如果采用密码登录方式需要在这里设置
- ***SSH Key File***
    表示是ssh 登录使用的密钥文件，如果是密钥方式在这里设置就可以
> ssh 既可以通过密码登录也可以通过密钥登录，二者取一就可以登录成功
- ***MySQL Hostname***
    表示数据库的内网地址，如果是本地就是127.0.0.1
- ***MySQL Server Port***
    表示数据库暴露的端口号，默认是3306
- ***Username***
    表示数据库的登录用户名
- ***Password***
    表示数据库的密码
















