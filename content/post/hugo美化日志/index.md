---
title: Hugo美化日志
date: 2024-02-23T13:39:00+08:00
draft: false
description: 这是描述位置
keywords: -hugo美化
image: cover.jpg
tags:
  - hugo美化
categories:
  - hugo相关
weight: 
lastmod: 2024-02-24
---

## 2024.02.23

### waline评论系统相关

**参考文章：**

[腾讯云cloudbase搭建waline评论系统](https://blog.z7sz.top/post/ffe060e9.html)

在[LeanCloud](https://console.leancloud.app/apps) 设置数据库（free,保存评论数据？），拿到相关密钥后去[Vercel](https://vercel.com/)部署服务端（free,让系统跑起来？）最后在网页中引入客户端（相当于app?）

一开始我把博客的库作为vercel的客户端了，导致后面评论管理端老是进不去。后来单独占用一个github私库就可以了。

~~刚才上线一看，好家伙评论客户端加载太慢了。改用国内腾讯的吧。~~**收费了**

还是用回免费的吧，我突然觉得速度也还过得去。。。



### 添加最后修改时间

### 文章为什么没有格式（无关本地是否有格式）
