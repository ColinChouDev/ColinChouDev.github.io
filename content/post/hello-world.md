---
title: "博客开始运行"
description: "这是博客的第一篇文章，也是 Hugo 与 Reimu 的基础使用说明。"
date: 2026-08-12T00:00:00+08:00
lastmod: 2026-08-12T00:00:00+08:00
draft: false
tags:
  - Hugo
  - 博客
categories:
  - 随笔
cover: "/images/banner-colin.jpg"
toc: true
math: false
mermaid: false
---

博客的第一版已经搭建完成。

它使用 Hugo 生成静态页面，文章以 Markdown 文件保存在 `content/post` 目录中。之后可以通过下面的命令创建新文章：

```sh
hugo new content post/my-new-post.md
```

新文章默认是草稿。完成后，将文章头部的 `draft` 改为 `false`，再执行构建即可发布。

## 本地预览

```sh
hugo server --buildDrafts
```

浏览器访问 `http://localhost:1313/`，即可预览博客。

## 正式构建

```sh
hugo --gc --minify
```

生成的网站位于 `public` 目录，可以部署到任意静态网站托管平台。
