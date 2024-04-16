---
title: IDEA玩法收集
date: 2024-04-11T10:43:23+08:00
lastmod: 2024-04-13
draft: false
image: cover.jpg
description: IDEA使用技巧收集
keywords: IDEA使用技巧
tags:
  - java
  - IDEA
categories:
  - 工作
slug: 745f511a
---

## 全局默认设置之设置maven（2023.3版本）
- 因为每一次创建新项目都要修改一下maven位置设置为本地自己安装的，很麻烦
1. 在idea的创建项目的欢迎界面有一个Customize中最下面的allSettings搜索maven进行设置即可
## 编码拼接
- ""内容太长可以使用+号换行再用""拼接即可
- 代码一行可以直接换行，对齐。
## IDEA工具快捷键
- 先选中对应**文件**，alt + insert(新建任何东西) 
- 退出任何窗口 esc
- 源码窗口最大化 ctrl + shift +f12
- 生成**main方法** psvm
- **输出语句** 先写字符串再 .sout 即可
- 运行代码 ctrl +shift +f10
- idea自动保存，自动编译
- 打开project窗口 alt + 1
- 查找类源码 双击shift 选择classes 切选项卡（切编辑窗口）alt + 左右
- 查看源码 选中一个单词按 ctrl + b
- **自动**生成变量 先写值再 .var 修改的地方用回车切换
- 红色下划线代表有错误（语法），黄色代表警告
- 删除一行 ctrl+y
- 复制当前一行到下一行 ctrl+d
- for循环 fori 用回车切换修改变量
- 在一个类中查找方法 ctrl + f12
- 单行注释 ctrl + /
- 多行注释 ctrl + shift  + /
- 多行编辑 按住alt 鼠标拖动对齐的修改处
- 快速实例化对象，类名.new.var
- 快速生成if 布尔类型值.if
- 快速生成get 和set 方法 alt + insert 
- 按住shift + home或者end 选中一行之后，你想换位置，你可以按住ctrl键加上上下箭头
- 自动纠错：将鼠标移动到提示位置，按住alt + enter 出现选择
- 方法重写，ctrl+o
- 不知道参数写什么时，可以按CTRL + p
- 给代码块生成控制语句快捷键：ctrl + alt + t

