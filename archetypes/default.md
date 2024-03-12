---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod:
draft: true
image: cover.jpg
description: 这是标题下面
keywords: 关键词优化SEO
tags:
  - html
  - themes
categories:
  - themes
  - syntax
slug: {{ substr (md5 (printf "%s%s" .Date (replace .TranslationBaseName "-" " " | title))) 4 8 }}
---

