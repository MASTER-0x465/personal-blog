# 个人博客

一个基于 [Astro](https://astro.build) 的纯静态个人博客，用于分享技术文章。

## 本地开发

```bash
npm install
npm run dev
```

打开 http://localhost:4321 即可预览，改代码会自动热更新。

## 写新文章

在 `src/content/blog/` 下新建一个 `.md` 文件，例如 `my-post.md`：

```markdown
---
title: 文章标题
description: 一句话摘要（会显示在文章卡片上）
pubDate: 2026-08-25
tags: ["后端", "数据库"]
---

正文内容，支持 Markdown。
```

保存后首页和文章列表会自动出现这篇文章。

## 构建

```bash
npm run build
```

构建产物输出到 `dist/` 目录。

## 部署到 Cloudflare Pages

1. 把本项目推送到 GitHub：

   ```bash
   git init
   git add .
   git commit -m "init blog"
   git remote add origin <你的仓库地址>
   git push -u origin main
   ```

2. 打开 [Cloudflare Pages](https://dash.cloudflare.com/)，点击 **Create a project** → **Connect to Git**，选择刚推送的仓库。
3. 构建配置按默认即可：构建命令 `npm run build`，输出目录 `dist`。
4. 点击 **Save and Deploy**，几分钟后就能拿到 `xxx.pages.dev` 的访问地址。

以后每次推送到 GitHub，Cloudflare 会自动重新构建部署。

## 绑定自定义域名

1. 在 Cloudflare Pages 项目设置 → **Custom domains** 中添加你的域名。
2. 按提示在域名服务商处添加 CNAME 记录，指向 `xxx.pages.dev`。
3. HTTPS 证书由 Cloudflare 自动签发，无需自己配置。

## 已实现的功能

- RSS 订阅：`/rss.xml`
- 标签页与按标签筛选：`/tags`
- 站内搜索：`/search`（内置轻量搜索，无需额外依赖）
- 评论（Giscus）：文章页底部，评论存储在 GitHub Discussions
- 访问统计：推荐使用 Cloudflare Web Analytics（后台一键开启，无需改代码）

### Giscus 评论启用步骤

1. GitHub 仓库 → Settings → Features → 打开 **Discussions**
2. 打开 [giscus.app](https://giscus.app)，选择该仓库，生成配置
3. 把 `src/components/Giscus.astro` 里的 `REPO_ID` 和 `CATEGORY` 替换成生成的值
4. 推送到 main 分支即可生效

### 访问统计启用步骤

1. Cloudflare 后台 → Analytics & Logs → **Web Analytics**
2. **Add a site** → 选择 masterwn.com（站点已在 Cloudflare 上，自动接入，无需改代码）

### 写文章模板

```markdown
---
title: 文章标题
description: 一句话摘要（会显示在文章卡片上）
pubDate: 2026-08-27
tags: ["后端", "数据库"]
---

正文内容，支持 Markdown。
```