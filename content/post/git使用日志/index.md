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
lastmod: 2024-04-04
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
**是的，在你不提交修改时切换分支，会提醒你提交修改。**
1. 在主分支合并使用快速模式导致日志不会出现分支合并历史。
## 添加版本标签
1. `git tag [选项] <标签名> [提交哈希]`
2. **选项**
- `-a`：在创建标签时，自动生成 GPG 签名。
- `-f`：强制更新已存在的标签。
- `-m`：指定标签的注释信息。
- `-s`：在创建标签时，使用 GPG 签名。
```
# 创建一个名为 v1.0.0 的标签 
git tag v1.0.0 
# 创建一个名为 v2.0.0 的标签，并附带注释信息 
git tag -m "This is the v2.0.0 release" v2.0.0 
# 强制更新 v1.0.0 标签 
git tag -f v1.0.0 
# 创建一个名为 v3.0.0 的签名标签 
git tag -s v3.0.0
```
### **查看标签**
可以使用 `git tag` 命令查看所有标签。
```
git tag
```
### **删除标签**
可以使用 `git tag -d` 命令删除标签。
```
# 删除 v1.0.0 标签
git tag -d v1.0.0
```
### **推送标签**
要将标签推送到远程仓库，可以使用 `git push` 命令。
```
# 将所有标签推送到远程仓库
git push origin --tags

# 将 v2.0.0 标签推送到远程仓库
git push origin v2.0.0
```
### **使用标签**
可以使用标签来检出特定的版本。
```
# 检出 v1.0.0 版本
git checkout v1.0.0

# 检出 v2.0.0 版本
git checkout v2.0.0
```
- **推送标签和推送最新修改是分开的**