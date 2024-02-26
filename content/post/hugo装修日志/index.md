---
title: Hugo装修日志
date: 2024-02-23T13:39:00+08:00
draft: false
description: 磕磕碰碰的装修
keywords: hugo美化
image: cover.jpg
tags:
  - hugo美化
categories:
  - hugo
weight:
---

## 2024.02.23

### 添加waline评论系统

**参考文章：**

[waline快速上手](https://waline.js.org/guide/get-started/)

在[LeanCloud](https://console.leancloud.app/apps) 设置数据库（free,保存评论数据？），拿到相关密钥后去[Vercel](https://vercel.com/)部署服务端（free,让系统跑起来？）最后在网页中引入客户端（相当于app?）

一开始我把博客的库作为vercel的客户端了，导致后面评论管理端老是进不去。后来单独占用一个github私库就可以了。**评论系统是用不了，虽然可以看到客户端。**
## 2024.02.24
### 添加最后修改时间
**参考文章：**
[hugo中文文档](https://hugo.opendocs.io/getting-started/configuration/#configure-dates
直接在front Matter中设置lastmod字段即可（但是不会自动修改，每次改动需要手动修改一下）
**自动修改方案：**
在站点配置文件config中，添加以下代码即可：
```
# 自动更新最后修改时间 
enableGitInfo: true # 从git文件中获取相关信息
frontmatter:
  lastmod:
    - :git
    - :fileModTime
    - lastmod
    - :defalut
```
把文章和文章模板中的lastmod字段删除掉。

**obsidian中有关dataview插件设置：**
因为插件中我用了lastmod字段作为文件显示在面板中，删除后意味着最后修改时间无法显示改用一下代码：
```
//### 草稿箱
//```dataview
//table title AS "标题",date AS "创建时间",file.mtime AS "最后修改"
//from "content/post"
//where draft=true
//sort date desc
//```

//### 已发布
//```dataview
//table title AS "标题",date AS "创建时间",file.mtime AS "最后修改"
//from "content/post"
//where draft=false
//sort date desc
//```
```
使用时把"//"去掉即可。
### 文章行首缩进

**参考文章：**
[行首缩进](https://www.syfly007.com/post/CS/site/hugo%E7%BD%91%E7%AB%99%E6%90%AD%E5%BB%BA.html#%E8%A1%8C%E9%A6%96%E7%BC%A9%E8%BF%9B)
使段落行首自动缩进2个空格(针对我的stack主题我的路径为\themes\hugo-theme-stack\assets\scss\partials，避免主题更新的问题文件我复制一份出来用于覆盖了)

修改相关scss文件，增加段落样式
```
.article-content p {
    text-indent: 2em;
}
```
还有代码缩进我感觉主题本身还不错就没有改了。
### 生成永久链接
**参考文章：**
[永久链接生成方案](https://blog.lxdlam.com/post/9cc3283b/#:~:text=%E4%BF%AE%E6%94%B9%20archetypes%2Fdefault.md%20%E6%B7%BB%E5%8A%A0%E5%A6%82%E4%B8%8B%E4%B8%80%E8%A1%8C%EF%BC%9A%201%202%203%204%205,hugo%20new%20%E7%9A%84%E6%97%B6%E5%80%99%E5%B0%B1%E4%BC%9A%E8%87%AA%E5%8A%A8%E5%A1%AB%E5%86%99%E4%B8%80%E4%B8%AA%E6%B0%B8%E4%B9%85%E9%93%BE%E6%8E%A5%E4%BA%86%E3%80%82%20%E4%B9%8B%E5%90%8E%E4%BF%AE%E6%94%B9%20config.toml%20%E6%B7%BB%E5%8A%A0%E5%A6%82%E4%B8%8B%E8%A1%8C%EF%BC%9A%20post%3D%22%2Fpost%2F%3Aslug%22%20%E7%94%9F%E6%88%90%E7%AB%99%E7%82%B9%E5%B0%B1%E5%8F%AF%E4%BB%A5%E4%BA%86%E3%80%82)
## 2024.02.26

### 修改标签和分类框的样式和页面底色
**相关参数在scss文件中有,直接修改即可。**
修改文件夹中此文件 /themes/hugo-theme-stack/assets/scss/variables.scss`
```
--tag-border-radius: 18px;  #Change from 4px to make it round corner
--body-background:#F9F5F6; #背景改为自己喜欢的颜色
```
修改后如果出现个别页面颜色没有转变，可以清除一下缓存再重新加载一下hugo项目
```
hugo mod clean --all && hugo --cleanDestinationDir
```
### “博客已运行x天x小时x分钟”字样

[参考文章](https://thirdshire.com/hugo-stack-renovation/#%E5%8D%9A%E5%AE%A2%E5%B7%B2%E8%BF%90%E8%A1%8Cx%E5%A4%A9x%E5%B0%8F%E6%97%B6x%E5%88%86%E9%92%9F%E5%AD%97%E6%A0%B7)
### 总字数统计：“发表了x篇文章，共计x字”
[参考](https://thirdshire.com/hugo-stack-renovation/#%E5%8D%9A%E5%AE%A2%E5%B7%B2%E8%BF%90%E8%A1%8Cx%E5%A4%A9x%E5%B0%8F%E6%97%B6x%E5%88%86%E9%92%9F%E5%AD%97%E6%A0%B7)
加了两个部件之后，发现版权信息和这两个部件间隔有一点远，可以调整为：
```
.copyright {
        color: var(--accent-color);
        font-weight: bold;
        margin-bottom: 1px;
    }
```
### 外部链接后面会显示图标
[参考](https://thirdshire.com/hugo-stack-renovation/#%E5%A4%96%E9%83%A8%E9%93%BE%E6%8E%A5%E5%90%8E%E9%9D%A2%E4%BC%9A%E6%98%BE%E7%A4%BA%E5%9B%BE%E6%A0%87)
### 缩小归档页的分类卡片尺寸
**有一点大，看着不太舒服**
[参考](http://localhost:1313/archives/)
