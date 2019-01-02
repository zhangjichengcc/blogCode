---
title: GIT配置多账户
date: 2019-01-02 09:41:00
comments: true
toc: true
banner: /blog/2019/01/02/GIT多账户/banner.jpg
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

>注意： 若不存在.ssh文件夹，则需要手动新建.ssh文件夹(git默认访问该文件，路径为：C:\Users\ [username]\ .ssh),并将生成的id_rsa和id_rsa_pub文件置入。如下图所示：

![.ssh文件](git_2.jpg)

---

### 把对应的公钥上传到服务器

>本文以github为例，其他平台类似

GitHub添加SSH key的方式如下图所示：

![.github添加ssh](git_3.jpg)

---

### 在.ssh目录下创建config文件并完成相关配置(<span style="color: #f00">核心</span>)

>每个账号单独配置一个Host，每个Host要取一个别名，每个Host主要配置HostName和IdentityFile两个属性即可

>Host的名字可以取为自己喜欢的名字，不过这个会影响git相关命令，例如：
Host mygithub 这样定义的话，命令如下，即git@后面紧跟的名字改为mygithub
git clone git@mygithub:PopFisher/AndroidRotateAnim.git

|          params          |                                     description                                     |
|--------------------------|-------------------------------------------------------------------------------------|
| HostName                 | 这个是真实的域名地址                                                                |
| IdentityFile             | 这里是id_rsa的地址                                                                  |
| PreferredAuthentications | 配置登录时用什么权限认证--可设为publickey,password publickey,keyboard-interactive等 |
| User                     | 配置使用用户名                                                                      |

``` bash
#github server 个人
Host github
Hostname github.com
User git
IdentityFile ~/.ssh/id_rsa_github
```

### 执行测试命令测试是否配置成功（会自动在.ssh目录生成known_hosts文件把私钥配置进去）

>同样以github账户为例，其他账户类似：

执行`ssh -T git@github.com`命令，按提示输入yes，此时会在.ssh目录下生成known_hosts文件
>注：经测试，执行clone命令同样可以生成known_host文件

### clone 项目

#### 获得项目ssh地址
![获取地址](git_4.jpg)
#### clone 项目
![clone项目](git_5.jpg)

