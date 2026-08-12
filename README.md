# Colin Blog

基于 [Hugo](https://gohugo.io/) 和 [hugo-theme-reimu](https://github.com/D-Sketon/hugo-theme-reimu) 的个人技术博客。

## 本地开发

首次克隆仓库后初始化主题：

```sh
git submodule update --init --recursive
```

启动本地预览：

```sh
hugo server --buildDrafts
```

访问 `http://localhost:1313/`。

## 写文章

```sh
hugo new content post/my-new-post.md
```

文章保存在 `content/post`。发布前将 Front Matter 中的 `draft` 设置为 `false`。

## 构建

```sh
hugo --gc --minify
```

静态文件输出到 `public` 目录。

## 常用配置

- 站点信息：`hugo.toml`
- 主题设置：`config/_default/params.yml`
- 默认封面：`static/images/banner-colin.jpg`
- 头像：`static/avatar/avatar-colin.jpg`
- 个性化样式：`static/css/colin-blog.css`
- 关于页面：`content/about.md`
