---
title: Hugo写文章的方法
date: 2024-02-23T13:34:08+08:00
draft: false
image: cover.jpg
keywords: hugo写作方法
tags:
  - hugo写作
categories:
  - hugo
weight: 
description: 记录收集到的hugo写作方法
lastmod: 2024-02-27
---

## 2024.02.23

**参考文章：**
1. [Hugo 博客写作最佳实践](https://blog.zhangyingwei.com/posts/2022m4d11h19m42s28/)
2. [Obsidian + Hugo](https://quantick.dev/posts/obsidian-hugo/)
3. [Hexo 转 Hugo](https://yelleis.top/p/0c0306ab/)

兜兜转转这么久，心太累了，老是被各种问题卡住，又发现不了问题。最后还是选择用`Shell commands`插件来代替创建以及提交操作,其他文章推荐的方法尝试失败了。
我在打开本地预览的命令上出错了，不过好在有chatGPT，我是用git bash来打开本地hugo 服务器的，插件上是使用cmd命令，这就导致cmd命令找不到项目。正确的命令为：
```
start chrome http://localhost:1313/ & hugo server -D --source F:\privateData\my_yugo
```
关闭本地浏览后有一个小bug，只能结束运行端口，不能关闭浏览器中的标签页。
## 2024.03.05
关于obsidian代码高亮的用法：要不就直接复制进来让他自动识别代码语言或则点击插入代码块区域在上方三个点后面输入代码语言。此方法有助于代码在obsidian以及在hugo中可以高亮显示。