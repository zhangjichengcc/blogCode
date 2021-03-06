---
title: hexo常用指令
date: 2018-02-05 14:29:09
comments: true
toc: true
categories: "工具"
tag:
	- hexo
banner: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1538053636652&di=0db3bc68fbdb79830a01281e006c9200&imgtype=jpg&src=http%3A%2F%2Fimg1.imgtn.bdimg.com%2Fit%2Fu%3D3996696336%2C4120219149%26fm%3D214%26gp%3D0.jpg
tags:
    - hexo
description: 生命在于折腾，又把博客折腾到Hexo了。给Hexo点赞。
---

Welcome to [Hexo](https://hexo.io/)! 
<!--more-->

## 开始使用 Install

``` bash
$ npm install hexo -g     # 安装  
$ npm update hexo -g      # 升级  
$ hexo init             # 初始化 
```

## 快速开始 Quick Start

### 启动本地服务（查看效果）

``` bash
$ hexo server / $ hexo s
```
#### 服务器设置
``` bash
$ hexo server                        #Hexo 会监视文件变动并自动更新，您无须重启服务器。
$ hexo server -s                     #静态模式
$ hexo server -p 5000                #更改端口
$ hexo server -i 192.168.1.1         #自定义 IP
```

More info: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

``` bash
$ hexo generate / $ hexo g           #使用 Hexo 生成静态文件快速而且简单
$ hexo generate --watch              #监视文件变动
```

More info: [Generating](https://hexo.io/docs/generating.html)

### 文章发布
hexo 支持在github等平台上一键发布
注意： 经测试，该配置生效的条件为：
1. github 项目名要为你自己的github名 如：yourname.github.io 
2. github \_config.yml 文件的github配置如下
``` bash
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://yourname.github.io                   # url地址
root: /                                           # 根目录          
permalink: :year/:month/:day/:title/              # 链接组合
permalink_defaults:
·
·
·
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy: # 配置发布
  type: git
  repository: git@github.com:yourname/yourname.github.io.git # 配置为ssh地址，https会失败
  branch: master
```

``` bash
$ hexo deploy / $ hexo d
```

### 清空缓存及静态文件

``` bash
$ hexo clean
```

### 完成后部署

``` bash
$ hexo generate --deploy / hexo g --d
$ hexo deploy --generate / hexo d --g
```


### 创建模板
|   参数   |            描述            |
|----------|----------------------------|
| layout   | 布局                       |
| data     | 创建时间                   |
| title    | 标题                       |


| layout：参数 |     描述     |     存储路径    |             说明            |
|--------------|--------------|-----------------|-----------------------------|
| post         | 文章（默认） | source/\_posts   | 可以直接发布                |
| draft        | 草稿         | source          | 在source下新建一个文件夹    |
| page         | 页面         | source/\_drafts | 新建文件将保存到 \_drafts中 |


``` bash
$ hexo new [layout] <title>
```
#### 创建文章
``` bash
$ hexo new <title>
$ hexo new "postName" #新建文章
```
#### 创建页面
``` bash
$ hexo new page <pageName>
$ hexo new page "pageName" #新建页面
```
### 创建/发布草稿

#### 创建草稿
*会在source/_drafts目录下生成一个new-draft.md文件。但是这个文件不被显示在页面上，链接也访问不到。也就是说如果你想把某一篇文章移除显示，又不舍得删除，可以把它移动到_drafts目录之中。*

``` bash
$ hexo new draft "new draft"
```

*如果你希望强行预览草稿，更改配置文件 (_config.yml)：*

``` bash
render_drafts: true
```
*或者，如下方式启动 server：*
``` bash
$ hexo server --drafts
```

#### 发布草稿

``` bash
$ hexo pushlish [layout] <title>
$ hexo publish / $ hexo p
```

More info: [Writing](https://hexo.io/docs/writing.html)


### 指令组合执行 &

通常开发测试要依次执行 hexo clean => hexo generate => hexo server, 我们可以通过指令组合执行来完成

``` bash
hexo clean & hexo g & hexo s
```



More info: [Deployment](https://hexo.io/docs/deployment.html)
