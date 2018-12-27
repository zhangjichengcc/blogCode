---
title: GIT配置多账户
date: 2018-12-17 09:41:00
comments: true
toc: true
banner: /blog/2018/12/17/GITduozhanghu/git_1.jpg
categories: '随笔'
tags:
	- git
---

>如今git作为当下最火的版本控制工具，基本开发人员都会有多个git账户，如gitlab，github及码云等都是基于git。那么如何在同一台设备上管理多个git账户呢？一种是不做ssh的配置，此时每次push操作都要输入用户名密码，还有一种则是配置ssh-key，本文介绍如何在window系统下托管多个ssk-key来管理git账号。

<!--more-->

### 生成ssh私钥公钥

执行如下命令
``` js
ssh-keygen -t rsa -C email
```
如下图所示，根据你的email生成ssh并根据需要键入key名（最好是有含义的域名，如我的这个key用于github，则命名为id_res_github）

![生成ssh密钥](git_1.jpg)

6666

