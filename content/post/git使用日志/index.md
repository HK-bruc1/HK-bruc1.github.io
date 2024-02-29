---
title: Git使用日志
date: 2024-02-27T18:16:17+08:00
draft: false
image: cover.jpg
description: 记录一下常用的命令和配置以及遇到的问题
keywords: git美化
tags:
  - git相关
categories:
  - Git
slug: 78e24be7
---
## 日志美化
默认的日志不太直观，从网络上参考了一下做出了如下配置：
```
git config --global alias.lg 'log --color --graph --decorate --pretty=format:\'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset\' --abbrev-commit --all'
git config --global alias.slg 'log --color --graph --decorate --pretty=format:\'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset\' --abbrev-commit --all -n 10'
```
日志按如上配置后，日志太多会变成分页模式浏览日志具体操作如下：
1. 按空格向下翻一页
2. 按q退出分页模式
因为输入命令后窗口就是一页日志，只需空格即可，其他按键不需要。
## git合并问题
1. 分支修改后是否提交再到主分支合并提交合并信息后推送仓库？（合并后本地主分支会领先远程分支两个提交，感觉有一点重复操作）
2. 在主分支合并使用快速模式导致日志不会出现分支合并历史。