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

