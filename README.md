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

## 发布

确认文章内容后，提交并推送到 `main`：

```sh
git add content/post/my-new-post.md
git commit -m "publish my-new-post"
git push origin main
```

如果文章使用了新图片，也要将图片文件加入同一次提交。推送后，GitHub Actions 会自动构建并发布网站；可在仓库的 Actions 页面查看部署结果。

## 构建

```sh
hugo --gc --minify
```

静态文件输出到 `public` 目录。本地构建仅用于检查，不会单独更新线上网站。

## 常用配置

- 站点信息：`hugo.toml`
- 主题设置：`config/_default/params.yml`
- 默认封面：`static/images/banner-colin.jpg`
- 头像：`static/avatar/avatar.jpg`
- 个性化样式：`static/css/colin-blog.css`
- 关于页面：`content/about.md`
