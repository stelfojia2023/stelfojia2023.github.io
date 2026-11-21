# stelfojia2023.github.io

知行札记。Jerry 的个人博客，发布在 <https://stelfojia2023.github.io>。

站点使用 Jekyll，由 **GitHub Pages 从分支原生构建**（Settings > Pages > Source 选 Deploy from a branch）。仓库里没有自定义 GitHub Actions。启用的额外插件只有 Pages 支持的 `jekyll-feed`、`jekyll-seo-tag` 和 `jekyll-sitemap`。标签页和归档页用 Liquid 生成，不依赖白名单之外的插件。

本地依赖通过 `github-pages` gem 与 Pages 的构建环境对齐。

## 写一篇新文章

1. 在 `_posts` 目录新建文件，文件名必须是 `YYYY-MM-DD-title.md`。
   - 日期决定顺序，较新的文章出现在首页最上方。
   - `title` 是网址用的英文短名，用短横线连接。例如 `_posts/2026-11-21-how-to-publish.md`。
2. 在文件开头写上 front matter，至少包含 `title`、`date`、`tags`：

```yaml
---
layout: post
title: 文章标题
date: 2026-11-21 09:00:00 +0800
tags:
  - 标签一
  - 标签二
---
```

3. 用 Markdown 写正文。想自定义首页摘要时，在截断处单独插入一行 `<!-- more -->`。
4. 提交并推送到 `main` 分支。GitHub Pages 会自动构建并发布。

不准备公开的稿子可以放在 `_drafts`（文件名不必带日期），或在 front matter 里写 `published: false`。

标签会汇总到「标签」页，全部文章按年份汇总到「归档」页。RSS 地址是 <https://stelfojia2023.github.io/feed.xml>。

更细的说明见示例文章《如何发布一篇新文章》。

## 启用 GitHub Pages

如果网站还没有上线：

1. 打开仓库的 **Settings > Pages**。
2. 在 **Build and deployment** 中，**Source** 选择 **Deploy from a branch**。
3. Branch 选择 **main**，文件夹选择 **/ (root)**，然后保存。

这是用户站点，仓库名必须是 `stelfojia2023.github.io`，页面从域名根路径提供，因此 `_config.yml` 里的 `baseurl` 为空。保存后等构建完成，即可通过 <https://stelfojia2023.github.io> 访问。

构建由 GitHub 托管的 Pages 流水线完成。仓库中不需要添加 workflow 文件；Actions 列表里的 `pages-build-deployment` 是 GitHub 自己的构建记录。

## 本地预览

需要 Ruby 与 Bundler：

```bash
bundle install
bundle exec jekyll serve
```

浏览器打开 <http://127.0.0.1:4000>。只构建、不启动服务：

```bash
bundle exec jekyll build
```

生成结果在 `_site/`，该目录已写入 `.gitignore`。
