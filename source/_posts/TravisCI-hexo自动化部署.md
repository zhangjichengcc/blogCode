---
title: Travis CI + github + hexo 自动化部署
date: 2019-01-03 10:18:38
toc: true
categories: '随笔'
banner: /blog/2019/01/03/TravisCI-hexo自动化部署/banner.jpg
tags:
    - hexo
    - Travis
    - git    
    - 部署    
---

>[Travis CI](https://travis-ci.org/)是目前新兴的开源持续集成构建项目，采用`yaml`格式，简洁清新独树一帜。目前大多数的github项目都已经移入到Travis CI的构建队列中。Travis-CI会同步你在GitHub上托管的项目，每当你`commit` `push`成功之后，就可以根据配置文件进行项目的构建发布。

>本博客最开始采用手动部署，后来采用jenkins部署，但是配置步骤相对繁琐，后来发现了Travis CI，基于github刚好符合我的需求，并且配置起来十分方便，本文记录了配置Travis的全过程，构建步骤为：
>1. 本地开发完成，提交代码到github仓库;
2. github收到提交的更新，通知Travis;
3. Travis 收到github的提交通知，进行构建;

<!-- more -->

[Travis CI](https://travis-ci.org/)
![](https://img.shields.io/badge/version-v1.0-green.svg)
![](http://progressed.io/bar/91?title=done)
![](http://progressed.io/bar/99)

