---
title: 给Hexo博客添加访问统计
date: 2018-09-27 16:35:58
categories: 工具
tags: hexo
thumbnail: http://busuanzi.ibruce.info/images/garlic.png
---
导语： 引入不蒜子为你的博客添加访问量
<!--more-->
### 引入不蒜子
``` bash
<script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
这段代码可以写在footer.ejs里或者header.ejs里或者layout.ejs里

### 添加站点访问量
通常站点的总访问量会显示在footer的位置，所以我们可以在footer.ejs里加上如下标签：
``` bash
<span id="busuanzi_container_site_uv"> 
  本站访客数<span id="busuanzi_value_site_uv"></span>人次
</span>
```
计算访问量的方法有两种：
算法a：pv的方式，单个用户连续点击n篇文章，记录n次访问量。
算法b：uv的方式，单个用户连续点击n篇文章，只记录1次访客数。
我用的是uv的方式，大家自行选择即可。

### 添加文章访问量
文章的访问量显示在文章里面，所以在article.ejs里加上文章访问量的标签：
``` bash
<span id="busuanzi_container_page_pv">
   本文总阅读量<span id="busuanzi_value_page_pv"></span>次
</span>
```

参考 : [不蒜子](http://busuanzi.ibruce.info/)
