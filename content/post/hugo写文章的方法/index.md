---
title: Hugo写文章的方法
date: 2024-02-23T13:34:08+08:00
draft: false
image: cover.jpg
description: 记录找到的hugo写作的不同方式
keywords:
    -hugo写作
tags: 
    - hugo写作
categories:
    - hugo相关
weight:  # 
---



## 2024.02.23

1. 使用命令创建模板文件

```
hugo new post/title/index.md
```

2. 使用typora打开文件进行编辑

- 可以改front Matter的文章元数据
- 文章有标题不需要再写一个标题（从二级标题开始似乎效果好看一点）
- 封面和其他图片都可以放在对应title文件夹内
- 封面获取`https://unsplash.com/`

3. 写好直接push,CF自动部署
