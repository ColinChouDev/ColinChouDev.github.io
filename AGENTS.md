# AGENTS.md — Colin Blog 项目交接说明

本文件供后续在本仓库工作的代理阅读。开始任何任务前，先阅读本文件；用户的最新明确要求始终优先于本文。

## 1. 项目目标与当前状态

- 项目是 Colin 的个人博客，内容方向为计算机技术、编程与生活。
- 技术栈：Hugo + `hugo-theme-reimu`。
- 生产站点：<https://blog.colinchou.top/>。
- GitHub 仓库：`ColinChouDev/ColinChouDev.github.io`。
- 当前源码分支：`main`。
- 发布分支：`gh-pages`，由 GitHub Actions 自动生成；不要手工编辑。
- 托管平台：GitHub Pages，不需要单独服务器。
- 域名在腾讯云 DNSPod 管理，`blog.colinchou.top` 指向 GitHub Pages。
- 截至 2026-08-13，第一版已经完成上线验收，可以视为稳定版本。

## 2. 用户已经确认的产品决定

除非用户明确提出变更，否则不要主动恢复、增加或重新设计以下内容。

### 站点风格

- 以 Hugo Reimu 原版为基础，曾参考 `blog.z0z0r4.top` 的个性化思路，但不要求继续照搬。
- 保留深色、蓝色、星空背景和当前 Colin Blog 视觉风格。
- 首页横幅标题：`Colin Blog`。
- 首页标题下方副标题：`Code & Life`。
- 侧栏姓名下方宣言：`I want to get really rich`。
- 不在首页横幅显示上述侧栏宣言。
- 加载动画保留，但禁止显示“正在建立链接……”等文字提示。
- Favicon 使用当前 `static/favicon.ico`，不要恢复主题默认图标。

### 导航与侧栏

- 顶部和侧栏导航只保留：首页、归档、关于、友链。
- 不需要“存档点”按钮及其功能。
- 侧栏作者区保留头像、名字、宣言、文章/分类/标签数量、邮箱和 GitHub。
- 侧栏组件只保留“分类”和“标签”，并且仅在首页显示；其他页面不显示这两个组件。
- 标题应叫“标签”，不要叫“标签云”。
- 不显示单独的普通“标签列表”组件。
- 不显示“最新文章”组件。
- 导航页标题使用英文：`Archives`、`About`、`Friends`。
- 归档页已经按年份分组，文章日期只显示月日，格式为 `MM-DD`。

### 内容与联系信息

- 作者：`Colin`。
- GitHub：<https://github.com/ColinChouDev>。
- 邮箱：`colinchoudev@gmail.com`。
- 头像：`static/avatar/avatar.jpg`。
- 当前默认横幅和文章封面：`static/images/banner-colin.jpg`。
- About 页面已重写为自然、简洁的中文自我介绍，不要恢复旧版或模板示例。
- 友链页本站信息：
  - name: `Colin Blog`
  - owner: `Colin`
  - url: `https://blog.colinchou.top/`
  - desc: `Code & Life`
  - image: `https://blog.colinchou.top/avatar/avatar.jpg`

### 评论与访问统计

- 评论系统使用 Giscus，数据存放在仓库 GitHub Discussions 的 `Announcements` 分类中。
- Giscus 已经在线验证正常；不要把它替换成 Twikoo、Disqus 等系统，除非用户明确要求。
- 页脚访问统计使用主题默认的“不蒜子”2.3。
- 正式域名的 PV/UV 可作为趣味性趋势参考，不代表精确真人数量。
- `localhost:1313` 下不蒜子可能显示八千万级共享/错误数字，这不是线上站点数据。
- 线上曾实测约为 PV 45、UV 25；数字会随访问变化，不能把这个值写死。
- 用户目前没有要求修改统计实现。若以后优化，优先建议只在正式域名显示，或换成拥有后台/明细的统计工具；不要擅自改动。

## 3. 重要文件

- `hugo.toml`：站点基础配置、正式域名、语言与输出格式。
- `config/_default/params.yml`：Reimu 主题主要配置、菜单、作者、侧栏、评论和统计。
- `content/post/`：博客文章。
- `content/about.md`：About 页面。
- `content/friend.md`：友链页面。
- `content/archives/_index.md`：归档页元数据。
- `layouts/partials/footer.html`：页脚覆盖模板。
- `layouts/partials/sidebar/commonBar.html`：侧栏覆盖模板。
- `i18n/zh-CN.yml`：中文文案与页面标题覆盖。
- `static/css/colin-blog.css`：主要个性化样式。
- `static/avatar/avatar.jpg`：当前头像。
- `static/images/banner-colin.jpg`：当前横幅和默认封面。
- `static/favicon.ico`：浏览器标签页图标。
- `static/CNAME`：必须保持为 `blog.colinchou.top`。
- `.github/workflows/deploy.yml`：自动构建并部署到 `gh-pages`。
- `themes/hugo-theme-reimu`：Git submodule，当前基于 Reimu v0.16.1 附近版本。

优先通过站点根目录的配置、`layouts` 覆盖和 `static/css/colin-blog.css` 定制。不要直接修改主题 submodule，除非任务明确要求升级或修复主题本身。

## 4. 本地开发与验证

首次克隆后：

```sh
git submodule update --init --recursive
```

启动本地预览：

```sh
hugo server --buildDrafts
```

访问：<http://localhost:1313/>。

生产构建：

```sh
HUGO_CACHEDIR=/tmp/colin-blog-hugo-cache hugo --gc --minify --cleanDestinationDir
```

在受限环境里不要直接依赖 Hugo 默认的 `~/Library/Caches`，否则可能遇到缓存目录权限错误。生产构建成功时，当前规模约为 20 个页面和 197 个静态文件；数量会随文章增加而变化。

每次涉及页面展示或交互的修改，至少验证：

1. 首页能正常显示标题、副标题、文章卡片和侧栏。
2. 移动端没有横向溢出，导航菜单可用。
3. `首页 → 归档 → 博客开始运行` 能正常跳转。
4. `About`、`Friends`、`Archives` 标题仍为英文。
5. 文章和普通页面的 Giscus 评论区可以加载。
6. 浏览器控制台没有与本站代码相关的 error/warn。
7. `static/CNAME` 仍为正式域名。
8. `git diff --check` 通过，且没有误提交 `public/`、`resources/` 或缓存文件。

## 5. 发布文章

创建文章：

```sh
hugo new content post/article-name.md
```

编辑 `content/post/article-name.md`，发布前把 Front Matter 中的 `draft` 改为 `false`，然后：

```sh
git add .
git commit -m "publish article-name"
git push origin main
```

推送 `main` 后，GitHub Actions 会使用 Hugo `0.164.0 extended` 构建，并强制更新 `gh-pages`。不要把生成的 `public/` 提交到 `main`。

## 6. Git 与部署约束

- 当前采用一个仓库、两个核心分支：`main`（源码）和 `gh-pages`（生成站点）。
- `.gitignore` 已忽略 `/public`、`/resources`、`.hugo_build.lock`、`.DS_Store`、IDE 与环境文件。
- 工作区可能包含用户或其他代理的改动；开始修改前先运行 `git status --short`，不要覆盖无关更改。
- 不要使用 `git reset --hard`、强制覆盖源码分支或手工编辑 `gh-pages`。
- 不要提交密钥、令牌或本地环境文件。
- 最近一次已验收的功能提交为 `1bd377a show sidebar widgets only on home page`；项目交接说明已通过 `f2520df add project agent guide` 纳入版本控制，后续提交出现时以仓库现状为准。

## 7. 已完成的上线验收

2026-08-13 已完成以下检查：

- `main` 与 `origin/main` 对齐，工作区干净。
- Hugo 正式构建通过，无站点构建错误。
- GitHub Actions 最新部署成功。
- `blog.colinchou.top`、HTTPS 和自定义域名正常。
- 首页、归档、About、友链、文章页正常。
- 桌面与 430px 左右移动端布局正常，无横向溢出。
- PJAX 导航正常。
- Giscus iframe 正常加载并映射到 GitHub Discussions。
- 线上浏览器控制台无相关错误或警告。

## 8. 后续工作原则

- 第一版已经完成，默认目标是稳定维护和发布内容，而不是持续重构。
- 用户经常先要求“商讨，不写代码”。遇到此类请求只分析，不修改文件。
- 用户要求“参考”其他博客时，提取思路即可；在没有明确同意前不要整页照搬。
- 修改视觉细节前先观察桌面端和移动端当前效果，尽量做最小改动。
- 恢复主题默认行为时，应先说明原版代码逻辑，不要以“优化”为由改变默认点。
- 涉及 PV/UV 时必须区分正式域名和 localhost，不要把本地异常数字解释成真实流量。
- 最终回复应明确：修改了什么、验证了什么、是否需要用户进行额外操作。
