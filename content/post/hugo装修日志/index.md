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
---

## 装修计划
- [ ] 代码块部分的高亮与背景以及代码行数不对齐问题
- [ ] 评论系统要整一个只需要一个昵称就可以的
- [x] bug1：最后修改时间似乎随着git提交时间全部刷新
- [ ] 滚动条样式
- [ ] 霞鹜文楷等宽字体上传到cdnjs
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
**有一点大，看着不太舒服**[参考](https://thirdshire.com/hugo-stack-renovation/#%E7%BC%A9%E5%B0%8F%E5%BD%92%E6%A1%A3%E9%A1%B5%E7%9A%84%E5%88%86%E7%B1%BB%E5%8D%A1%E7%89%87%E5%B0%BA%E5%AF%B8) 
## 2024.02.29
### 文章增加字数统计
[参考](https://coderqs.github.io/2022/02/hugo-stack-%E4%B8%BB%E9%A2%98%E8%A3%85%E4%BF%AE%E7%AC%94%E8%AE%B0/#%E5%A2%9E%E5%8A%A0%E6%96%87%E7%AB%A0%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1)
### 把最后修改时间放到页面上
文章页面底部的布局位于 `{{ partial "article/components/footer" . }}` 在这个html文件中。直接把lastmod相关代码截取放到layouts/partials/article/components/details.html文章创建时间的后面。
由于相关标签定义了css样式（assets\scss\partials\layout\article.scss的.article-lastmod中），导致跟其他部件样式不一致，简单起见就是直接把定位的标签改掉。让默认布局覆盖。修改之后的代码为：

```
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
```
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
```
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
### bug1：
如果在分支中修改了文件，然后将分支合并到主分支，并且使用了 --no-ff 参数，那么主分支中所有文件的最后修改时间都将是合并时间。（所以在主题美化完成之前最后修改时间都是不正常的。）
### 字体样式的修改
**参考文章：**
[CDN使用LXGW WenKai Mono](https://shuilanjiao.gitee.io/p/2023/11/hugo-stack-lxgwwenkai/#cdn%E4%BD%BF%E7%94%A8lxgw-wenkai-mono)
[字体样式修改](https://xrg.fj.cn/p/hugo-stack%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%96%B0%E5%B0%8F%E8%AE%B0/#%E5%AD%97%E4%BD%93%E6%A0%B7%E5%BC%8F%E4%BF%AE%E6%94%B9)
[hugo自定义全局字体](https://blog.gezi.men/p/hugo-custom-global-font/)
[字体分包部署与使用](https://chinese-font.netlify.app/post/deploy_to_cdn/)
[github上的cdn链接](https://github.com/lxgw/LxgwWenKai/issues/24)
作者在layouts/partials/footer/components/custom-font.html 中进行了字体的自定义。引入了Lato 字体系列，在variables.scss文件中其实有多种字体但是我没找到引入的文件（也可能没有引入）。作者使用 Google Fonts 来引入字体。
如果需要针对特定页面或组件进行字体自定义，则建议将自定义字体添加到 layouts/partials/footer/components/custom-font.html 中。
如果希望全局应用字体自定义，则建议将自定义字体添加到 layouts/partials/head/custom.html 中。
**由于中文网字计划的 CDN 被多个平台盗用，故未来将缩减提供公共 CDN 链接的相应流量，并且不再保证链接稳定性。所以各位开发者需要自行将字体部署至 CDN 中，为各位的网页加速**。我在[github](https://github.com/lxgw/LxgwWenKai/issues/24)（两个链接都使用了国内镜像）上看到了该字体已经被其他人上传到cdnjs了（有两个版本按需求选择即可）。一般来说，cdnjs上的字体文件都是由可靠的上传者上传的，并且cdnjs服务也是比较可靠的。因此，可以放心使用其他人上传的CDN链接。
**我的步骤如下：** 复制提供的CDN链接，添加到主题目录\layouts\partials\head\custom.html中：
```
<!-- 引入霞鹜文楷字体 -->
<link rel='stylesheet' href='https://cdn.staticfile.org/lxgw-wenkai-screen-webfont/1.6.0/style.css' /> 
```
然后打开主题目录\assets\scss\variables.scss文件，找到:root并设置字体即可：
```
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
原来字体的配置可以保留，以防cdn链接失效导致渲染错误。配置保存后结束本地服务器重启项目即可。

