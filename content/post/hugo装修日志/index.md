---
title: Hugo装修日志
date: 2024-02-23T13:39:00+08:00
draft: false
description: 只记录参考出处以及遇到的问题
keywords: hugo美化
image: cover.jpg
tags:
  - hugo美化
categories:
  - hugo
weight: 
lastmod: 2024-03-05
---

## 装修计划
- [ ] 代码块部分的高亮与背景以及代码行数不对齐问题
- [ ] 评论系统要整一个只需要一个昵称就可以的
- [ ] 滚动条样式
- [ ] 霞鹜文楷等宽字体上传到cdnjs
- [ ] 代码块也改成圆角的
- [ ] 归档页面文章的简介没有
- [ ] 相册功能（能加一下文字说明呢？）
- [ ] 右侧有搜索了，能不能把左侧菜单的搜索删除
## 2024.02.23
### 添加waline评论系统
**参考文章：**
[waline快速上手](https://waline.js.org/guide/get-started/)
在[LeanCloud](https://console.leancloud.app/apps) 设置数据库（free,保存评论数据？），拿到相关密钥后去[Vercel](https://vercel.com/)部署服务端（free,让系统跑起来？）最后在网页中引入客户端（相当于app?）
一开始我把博客的库作为vercel的客户端了，导致后面评论管理端老是进不去。后来单独占用一个github私库就可以了。**评论系统是用不了，虽然可以看到客户端。**
## 2024.02.24
### 添加最后修改时间
**参考文章：**
[hugo中文文档](https://hugo.opendocs.io/getting-started/configuration/#configure-dates)
直接在front Matter中设置lastmod字段即可（但是不会自动修改，每次改动需要手动修改一下）
~~**自动修改方案：**~~ **本地显示正常但是用Cloudflare部署时会把所有文件的最后修改时间变成最近一次提交时间。**
在站点配置文件config中，添加以下代码即可： 
```yaml
# 自动更新最后修改时间 
# enableGitInfo: true # 从git文件中获取相关信息
frontmatter:
  lastmod:
    # - :git
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
使段落（需要空一行才会识别为新段落）行首自动缩进2个空格(针对我的stack主题我的路径为\themes\hugo-theme-stack\assets\scss\partials，避免主题更新的问题文件我复制一份出来用于覆盖了)
修改相关scss文件，增加段落样式
```scss
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
```scss
--tag-border-radius: 18px;  #Change from 4px to make it round corner
--body-background:#F9F5F6; #背景改为自己喜欢的颜色
```
修改后如果出现个别页面颜色没有转变，可以清除一下缓存再重新加载一下hugo项目
```go
hugo mod clean --all && hugo --cleanDestinationDir
```
### “博客已运行x天x小时x分钟”字样
[参考文章](https://thirdshire.com/hugo-stack-renovation/#%E5%8D%9A%E5%AE%A2%E5%B7%B2%E8%BF%90%E8%A1%8Cx%E5%A4%A9x%E5%B0%8F%E6%97%B6x%E5%88%86%E9%92%9F%E5%AD%97%E6%A0%B7)
### 总字数统计：“发表了x篇文章，共计x字”
[参考](https://thirdshire.com/hugo-stack-renovation/#%E5%8D%9A%E5%AE%A2%E5%B7%B2%E8%BF%90%E8%A1%8Cx%E5%A4%A9x%E5%B0%8F%E6%97%B6x%E5%88%86%E9%92%9F%E5%AD%97%E6%A0%B7)
加了两个部件之后，发现版权信息和这两个部件间隔有一点远，在同一文件中可以调整为：
```scss
.copyright {
        color: var(--accent-color);
        font-weight: bold;
        margin-bottom: 1px;
    }
```
### 外部链接后面会显示图标
[参考](https://thirdshire.com/hugo-stack-renovation/#%E5%A4%96%E9%83%A8%E9%93%BE%E6%8E%A5%E5%90%8E%E9%9D%A2%E4%BC%9A%E6%98%BE%E7%A4%BA%E5%9B%BE%E6%A0%87)
### 缩小归档页的分类卡片尺寸
**有一点大，看着不太舒服**[参考](https://thirdshire.com/hugo-stack-renovation/#%E7%BC%A9%E5%B0%8F%E5%BD%92%E6%A1%A3%E9%A1%B5%E7%9A%84%E5%88%86%E7%B1%BB%E5%8D%A1%E7%89%87%E5%B0%BA%E5%AF%B8) 
## 2024.02.29
### 文章增加字数统计
[参考](https://coderqs.github.io/2022/02/hugo-stack-%E4%B8%BB%E9%A2%98%E8%A3%85%E4%BF%AE%E7%AC%94%E8%AE%B0/#%E5%A2%9E%E5%8A%A0%E6%96%87%E7%AB%A0%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1)
### 把最后修改时间放到页面上
文章页面底部的布局位于 `{{ partial "article/components/footer" . }}` 在这个html文件中。直接把lastmod相关代码截取放到layouts/partials/article/components/details.html文章创建时间的后面。
由于相关标签定义了css样式（assets\scss\partials\layout\article.scss的.article-lastmod中），导致跟其他部件样式不一致，简单起见就是直接把定位的标签改掉。让默认布局覆盖。修改之后的代码为：

```html
<footer class="article-time">
        {{ if $showDate }}
            <div>
                {{ partial "helper/icon" "date" }}
                <time class="article-time--published">
                    {{- .Date.Format (or .Site.Params.dateFormat.published "Jan 02, 2006") -}}
                </time>
            </div>
        {{ end }}
		
		{{- if ne .Lastmod .Date -}}
			<div>
				{{ partial "helper/icon" "update" }}
				<time class="article-update">
					{{- .Lastmod.Format ( or .Site.Params.dateFormat.lastUpdated "Jan 02, 2006 15:04 MST" ) -}}
				</time>
			</div>
		{{- end -}}
		
		<div>
			{{ partial "helper/icon" "brush" }}
			<time class="article-words">
			{{ T "article.wordCount" .WordCount }}
			</time>
		</div>
	  
        {{ if $showReadingTime }}
            <div>
                {{ partial "helper/icon" "clock" }}
                <time class="article-time--reading">
                    {{ T "article.readingTime" .ReadingTime }}
                </time>
            </div>
        {{ end }}
    </footer>
```
标签由article-lastmod改为article-update，把代码形式修改成跟这几个部件一样即可应用他们相同的部件。
### 左侧边栏元素居中
样式在assets\scss\partials\sidebar.scss,在三个位置添加相同的配置，因为不太熟悉，也不敢乱作简化。
第一个位置：
```scss
.left-sidebar {
    display: flex;
    flex-direction: column; /* 保持垂直布局 */
	justify-content: center; /* 水平居中子元素 */
	align-items: center; /* 可选地，垂直居中元素 */
    flex-shrink: 0;
    align-self: stretch;
    gap: var(--sidebar-element-separation);
    max-width: none;
    width: 100%;
    position: relative;

    --sidebar-avatar-size: 100px;
    --sidebar-element-separation: 20px;
    --emoji-size: 40px;
    --emoji-font-size: 20px;

    @include respond(md) {
        width: auto;
        padding-top: var(--main-top-padding);
        padding-bottom: var(--main-top-padding);
        max-height: 100vh;
    }
```
第二个：
```scss
.sidebar header {
	display: flex;
	flex-direction: column; /* 保持垂直布局 */
	justify-content: center; /* 水平居中子元素 */
	align-items: center; /* 可选地，垂直居中元素 */
    z-index: 1;
    transition: box-shadow 0.5s ease;
    display: flex;
    flex-direction: column;
    gap: var(--sidebar-element-separation);

    @include respond(md) {
        padding: 0;
    }

    .site-avatar {
        position: relative;
        margin: 0;
        width: var(--sidebar-avatar-size);
        height: var(--sidebar-avatar-size);
        flex-shrink: 0;

        .site-logo {
            width: 100%;
            height: 100%;
            border-radius: 100%;
            box-shadow: var(--shadow-l1);
        }

        .emoji {
            position: absolute;
            width: var(--emoji-size);
            height: var(--emoji-size);
            line-height: var(--emoji-size);
            border-radius: 100%;
            bottom: 0;
            right: 0;
            text-align: center;
            font-size: var(--emoji-font-size);
            background-color: var(--card-background);
            box-shadow: var(--shadow-l2);
        }
    }

    .site-meta {
        display: flex;
        flex-direction: column;
        gap: 10px;
        justify-content: center;
    }

    .site-name {
		display: flex;
		flex-direction: column; /* 保持垂直布局 */
		justify-content: center; /* 水平居中子元素 */
		align-items: center; /* 可选地，垂直居中元素 */
        color: var(--accent-color);
        margin: 0;
        font-size: 1.6rem;

        @include respond(2xl) {
            font-size: 1.8rem;
        }
    }

    .site-description {
        color: var(--body-text-color);
        font-weight: normal;
        margin: 0;
        font-size: 1.4rem;

        @include respond(2xl) {
            font-size: 1.6rem;
        }
    }
}
```
实现效果就是菜单居中，头像和站点名称居中了。
## 2024.03.02
### 代码块引入MacOS窗口样式
[参考文章](https://blog.linsnow.cn/p/modify-hugo/#%E4%BB%A3%E7%A0%81%E5%9D%97%E5%BC%95%E5%85%A5macos%E7%AA%97%E5%8F%A3%E6%A0%B7%E5%BC%8F)
由于我的assets文件夹img文件夹但是我按照教程来发现不起作用。可能的原因为（回答来自Gemini）：
 webpack 处理 assets 文件夹中的文件的方式与处理 static 文件夹中的文件的方式不同:
- **assets 文件夹:** webpack 会将 assets 文件夹中的文件打包到最终的 bundle 文件中，需要使用 `require()` 或 `import()` 语句来引入。
- **static 文件夹:** webpack **不会** 处理 static 文件夹中的文件，会被直接复制到最终的输出目录中，可以直接在 HTML 代码中引用。
- assets 文件夹中的文件通常会被浏览器缓存，可能会导致更新文件后不立即显示更改。
### 加载进度条
[参考](https://yelleis.top/p/61fdb627/#%E5%8A%A0%E8%BD%BD%E8%BF%9B%E5%BA%A6%E6%9D%A1)
东西加多了是会有一点慢，考虑加一个不太显眼的加载条。
### 添加背景的蜘蛛网特效
[参考](https://ponder.lol/2023/custom-hugo-theme-stack/#%E6%B7%BB%E5%8A%A0%E8%83%8C%E6%99%AF%E7%9A%84%E8%9B%9B%E7%BD%91%E7%89%B9%E6%95%88)
暂时看来两者好像都不怎么慢，如果以后慢的话可以选者嵌入代码方式而不是使用外部脚本。
## 2024.03.04
### 字体样式的修改
**参考文章：**
[使用LXGW WenKai Mono](https://shuilanjiao.gitee.io/p/2023/11/hugo-stack-lxgwwenkai/#%E7%9B%B4%E6%8E%A5%E4%BD%BF%E7%94%A8lxgw-wenkai)
[字体样式修改](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/#%E5%AD%97%E4%BD%93%E6%A0%B7%E5%BC%8F%E4%BF%AE%E6%94%B9)
[hugo自定义全局字体](https://blog.gezi.men/p/hugo-custom-global-font/)
[字体分包部署与使用](https://chinese-font.netlify.app/post/deploy_to_cdn/)
[github上的cdn链接](https://github.com/lxgw/LxgwWenKai/issues/24)
作者在layouts/partials/footer/components/custom-font.html 中进行了字体的自定义。引入了Lato 字体系列，在variables.scss文件中其实有多种字体但是我没找到引入的文件（也可能没有引入）。作者使用 Google Fonts 来引入字体。
如果需要针对特定页面或组件进行字体自定义，则建议将自定义字体添加到 layouts/partials/footer/components/custom-font.html 中。
如果希望全局应用字体自定义，则建议将自定义字体添加到 layouts/partials/head/custom.html 中。
**由于中文网字计划的 CDN 被多个平台盗用，故未来将缩减提供公共 CDN 链接的相应流量，并且不再保证链接稳定性。所以各位开发者需要自行将字体部署至 CDN 中，为各位的网页加速**。我在[github](https://github.com/lxgw/LxgwWenKai/issues/24)（两个链接都使用了国内镜像）上看到了该字体已经被其他人上传到cdnjs了（有两个版本按需求选择即可）。一般来说，cdnjs上的字体文件都是由可靠的上传者上传的，并且cdnjs服务也是比较可靠的。因此，可以放心使用其他人上传的CDN链接。
**我的步骤如下：** ~~复制github上提供的CDN链接~~，添加到主题目录\layouts\partials\head\custom.html中：
```html
<!-- 引入霞鹜文楷字体 -->
<link rel='stylesheet' href='https://cdn.staticfile.org/lxgw-wenkai-screen-webfont/1.6.0/style.css' /> 
```
然后打开主题目录\assets\scss\variables.scss文件，找到:root并设置字体即可：
```scss
/**
*   Global font family 全局字体系列
*/
:root {
	/**
	* 系统字体系列
	*/
    --sys-font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Droid Sans", "Helvetica Neue";
	/**
	* 中文字体系列
	*/
    --zh-font-family: "PingFang SC", "Hiragino Sans GB", "Droid Sans Fallback", "Microsoft YaHei";
	/**
	* 基础字体系列
	* 使用系统字体系列作为基础，并添加中文字体系列和 sans-serif 作为备用
	*/
    --base-font-family: "LXGW WenKai Screen", "Lato", var(--sys-font-family), var(--zh-font-family), sans-serif;
	/**
	* 代码字体系列
	* 使用 Menlo 作为首选，并添加 Monaco、Consolas、"Courier New" 和中文字体系列作为备用
	*/
    --code-font-family: Menlo, Monaco, Consolas, "Courier New", var(--zh-font-family), monospace;
}
```
原来字体的配置可以保留，以防cdn链接失效导致渲染错误。配置保存后结束本地服务器重启项目即可。**最后还是用上了中文网字计划的cdn因为他的版本字体细一点，那个Screen版有一点粗不好看。**
## 2024.03.05
### 代码高亮样式
在官方文档中有默认配配置：
```yaml
markup:
  highlight:
    anchorLineNos: false
    codeFences: true
    guessSyntax: false
    hl_Lines: ""
    lineAnchors: ""
    lineNoStart: 1   #行从几开始
    lineNos: false   #是否显示行列
    lineNumbersInTable: true
    noClasses: true
    style: monokai   #代码样式
    tabWidth: 4
```
样式风格有两个链接可以进入选择 [Short snippets 简短片段](https://xyproto.github.io/splash/docs/all.html)以及 [Long snippets 长片段](https://xyproto.github.io/splash/docs/longer/all.html)应该是对应不同需求来选择。格式选择之后重启一下服务器打开开发者工具看一下是什么颜色。去主题目录\assets\scss\variables.scss文件找到代码块部分根据高亮风格修改一下外围的颜色：
```scss
/* 亮色主题下的代码块样式 */
[data-scheme="light"] {
    --pre-text-color: #272822;
    --pre-background-color: #faf4ed; /* 代码块外围颜色，跟高亮风格一致即可。 */
    @import "partials/highlight/light.scss"; /* 引入亮色主题的代码块样式 */
}

/* 暗色主题下的代码块样式 */
[data-scheme="dark"] {
    --pre-text-color: #f8f8f2;
    --pre-background-color: #272822; /* 代码块背景颜色 ，跟高亮风格一致即可*/
    @import "partials/highlight/dark.scss"; /* 引入暗色主题的代码块样式 */
}
```
### 目录项紧凑
**参考文章：**
[目录项紧凑](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/#%E7%9B%AE%E5%BD%95%E9%A1%B9%E7%B4%A7%E5%87%91)
由于主题目录项不满意的地方只有高度和目录项之间的距离所以改动的地方没有参考文章那么多。之改动：`#TableOfContents` 选择器底下的属性：
```scss
max-height: 75vh;  // 控制目录的最大高度（没改动）
li {
            margin: 10px 10px; //目录项之间的距离（只改动间隙）
            padding: 5px;

            & > ol,
            & > ul {
                margin-top: 10px;
                padding-left: 10px;
                margin-bottom: -5px;

                & > li:last-child {
                    margin-bottom: 0;
                }
            }
        }
```
### 返回顶部按钮
参考文章：[返回顶部](https://yelleis.top/p/61fdb627/#%E8%BF%94%E5%9B%9E%E9%A1%B6%E9%83%A8)
将代码添加到 `/layouts/partials/footer/custom.html` 文件和 `/themes/hugo-theme-stack/layouts/partials/footer/components/script.html` 文件的区别如下：
`/layouts/partials/footer/custom.html` 文件中的代码会在所有页面的底部渲染。
`/layouts/partials/footer/components/script.html` 文件中的代码只会显示在包含 `{{ partial "footer/components/script" }}` 代码的页面底部。
代码如下：

```html
<!--返回顶部按钮 -->
<a href="#" id="back-to-top" title="返回顶部"></a>
<!--返回顶部CSS -->
<style>
  #back-to-top {
    display: none; /* 默认隐藏 */
    position: fixed;/* 固定定位 */
    bottom: 20px; /* 距离底部 20 像素 */
    right: 55px;/* 距离右侧 55 像素 */
    width: 55px;/* 宽度 55 像素 */
    height: 55px;/* 高度 55 像素 */
    border-radius: 7px; /* 圆角半径 7 像素 */
    background-color: rgba(234, 234, 234, 0.5); /* 按钮颜色 rgba(64, 158, 255, 0.5) */
    box-shadow: var(--shadow-l2);/* 盒子阴影 var(--shadow-l2) */
    font-size: 30px;/* 字体大小 30 像素 */
    text-align: center;/* 文本居中 */
    line-height: 50px;/* 行高 50 像素 */
    cursor: pointer;/* 鼠标指针变为手型 */
  }

  #back-to-top:before {
    content: ' ';/* 内容为空 */
    display: inline-block;/* 显示方式为块级元素 */
    position: relative;/* 相对定位 */
    top: 0;/* 距离顶部 0 像素 */
    transform: rotate(135deg);* 旋转 135 度 */
    height: 10px;* 高度 10 像素 */
    width: 10px;/* 宽度 10 像素 */
    border-width: 0 0 2px 2px;/* 边框宽度：上 0 像素，右 0 像素，下 2 像素，左 2 像素 */
    border-color: var(--back-to-top-color);/* 边框颜色 var(--back-to-top-color) */
    border-style: solid; /* 边框样式为实线 */
  }

  #back-to-top:hover:before {
    border-color: #2674e0; /* 边框颜色 #2674e0 */
  }

  /* 在屏幕宽度小于 768 像素时，钮位置调整 */
  @media screen and (max-width: 768px) {
    #back-to-top {
      bottom: 20px;
      right: 20px;
      width: 40px;
      height: 40px;
      font-size: 10px;
    }
  }

  /* 在屏幕宽度大于等于 1024 像素时，按钮位置调整 */
  @media screen and (min-width: 1024px) {
    #back-to-top {
      bottom: 20px;
      right: 40px;
    }
  }

  /* 在屏幕宽度大于等于 1280 像素时，按钮位置调整 */
  @media screen and (min-width: 1280px) {
    #back-to-top {
      bottom: 20px;
      right: 55px;
    }
  }

  /* 目录显示时，隐藏按钮 */
  @media screen and (min-width: 1536px) {
    #back-to-top {
      visibility: hidden;
    }
  }
</style>
<!--返回顶部JS -->
<script>
    // 定义一个函数 backToTop，用于滚动页面到顶部
    function backToTop() {
        // 使用 scrollTo 方法将页面滚动到顶部，平滑效果取决于浏览器的默认行为
        window.scrollTo(0, 0);
    }

    // 当页面加载完成时执行以下代码
    window.onload = function() {
        // 获取当前滚动的垂直位置（兼容不同浏览器的写法）
        let scrollTop = this.document.documentElement.scrollTop || this.document.body.scrollTop;
        // 获取 ID 为 'back-to-top' 的元素，通常是一个返回顶部按钮
        let totopBtn = this.document.getElementById('back-to-top');
        if (scrollTop > 0) {
            // 如果页面滚动位置大于 0，则显示返回顶部按钮
            totopBtn.style.display = 'inline';
        } else {
            // 否则隐藏返回顶部按钮
            totopBtn.style.display = 'none';
        }
    }

    // 当页面滚动时执行以下代码
    window.onscroll = function() {
        // 获取当前滚动的垂直位置（兼容不同浏览器的写法）
        let scrollTop = this.document.documentElement.scrollTop || this.document.body.scrollTop;
        // 获取 ID 为 'back-to-top' 的元素
        let totopBtn = this.document.getElementById('back-to-top');
        if (scrollTop < 200) {
            // 如果滚动位置小于 200 像素，则隐藏返回顶部按钮
            totopBtn.style.display = 'none';
        } else {
            // 否则显示返回顶部按钮，并为按钮添加点击事件，点击时执行 backToTop 函数
            totopBtn.style.display = 'inline';
            totopBtn.addEventListener('click', backToTop, false);
        }
    }
</script>
```
## 2024.03.06
### 整体布局的调整
代码抄自[这里](https://www.blain.top/p/renovation/#%E6%95%B4%E4%BD%93%E8%87%AA%E5%AE%9A%E4%B9%89%E6%A0%B7%E5%BC%8F%E8%A1%A8%E6%96%87%E4%BB%B6)调整一些格式（按需求添加，没生效的也没有添加）。能找到的变量我都在variables.scss文件中修改。其他不想花时间找（主要不熟悉前端）索性都放在\scss\custom.scss文件中：
```scss
//------------------------------------------------------
// 修复引用块内容窄页面显示问题
a {
  word-break: break-all;
}
  
code {
  word-break: break-all;
}
//---------------------------------------------------
// 文章内容图片圆角阴影
.article-page .main-article .article-content {
  img {
    max-width: 96% !important;
    height: auto !important;
    border-radius: 8px;
  }
}
//------------------------------------------------
// 文章内容引用块样式
.article-content {
  blockquote {
    border-left: 6px solid #358b9a1f !important;
    background: #B2DFEE;//引用块颜色
  }
}
// ---------------------------------------
// 代码块基础样式修改（改成了圆角）
.highlight {
  max-width: 102% !important;
  background-color: var(--pre-background-color);
  padding: var(--card-padding);
  position: relative;
  border-radius: 20px;
  margin-left: -7px !important;
  margin-right: -12px;
  box-shadow: var(--shadow-l1) !important;

  &:hover {
    .copyCodeButton {
	  opacity: 1;
    }
  }

  // keep Codeblocks LTR
  [dir="rtl"] & {
    direction: ltr;
  }

  pre {
    margin: initial;
    padding: 0;
    margin: 0;
    width: auto;
  }
}
//-------------------------------------------
// 设置选中字体的区域背景颜色
//修改选中颜色
::selection {
  color: #fff;
  background: rgba(52, 73, 94, 0.5);
}
  
a {
  text-decoration: none;
  color: var(--accent-color);
  
  &:hover {
    color: var(--accent-color-darker);
  }
  
  &.link {
    color: #4288b9ad;
    font-weight: 600;
    padding: 0 2px;
    text-decoration: none;
    cursor: pointer;
  
    &:hover {
      text-decoration: underline;
    }
  }
}  
//-------------------------------------------------
//文章封面高度更改
.article-list article .article-image img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  
  @include respond(md) {
    height: 250px;
  }
  
  @include respond(xl) {
    height: 285px;
  }
}
//-------------------------------------------------------
//全局页面小图片样式微调（主要是归档页面的小图片变成圆角）
.article-list--compact article .article-image img {
  width: var(--image-size);
  height: var(--image-size);
  object-fit: cover;
  border-radius: 17%;
} 
//----------------------------------------------------
//固定代码块的高度（代码区域限制高度，超出改为滑动浏览）
.article-content {
  .highlight {
      padding: var(--card-padding);
      pre {
          width: auto;
          max-height: 20em;
      }
  }
}
```
### 去除归档页初始滤镜
刚开始以为是图片问题呢。。。
参考来自[这里](https://www.blain.top/p/renovation/#%E5%8E%BB%E9%99%A4%E5%BD%92%E6%A1%A3%E9%A1%B5%E5%88%9D%E5%A7%8B%E6%BB%A4%E9%95%9C)
### 添加右下角联系小气泡按钮
**参考文章：**
- [点击这里！](https://irithys.com/hugo-mod-1/#%e8%81%94%e7%b3%bb%e6%b0%94%e6%b3%a1)
文章很详细了，完美配置了！用了气泡之后怎么感觉速度慢了不少？这才三篇文章呢！！！加了气泡之后每一次本地修改加载都很慢。。。


