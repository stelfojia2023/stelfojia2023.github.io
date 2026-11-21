---
layout: post
title: 如何发布一篇新文章
date: 2026-11-21 09:00:00 +0800
tags:
  - 指南
  - 写作
---

在 `_posts` 目录新增一个 Markdown 文件，文件名写成 `YYYY-MM-DD-title.md`，开头写上 `title`、`date` 和 `tags`，提交并推送到 `main` 分支，GitHub Pages 就会把它发布出来。

<!-- more -->

这篇笔记是给站点主人自己看的。照着做，就能在「知行札记」上多一篇文章。

## 1. 新建文件

在仓库的 `_posts` 目录里新建 Markdown 文件。文件名必须是：

```text
YYYY-MM-DD-title.md
```

例如本文就是 `_posts/2026-11-21-how-to-publish.md`。

- `YYYY-MM-DD` 是日期。首页和归档都按它从新到旧排列。
- `title` 是网址里的英文短名，单词用短横线连接。它不必和中文标题相同。
- 不要把中文放进文件名，以免网址难读。

## 2. 写上文首信息

文件最开头用两行 `---` 包住 front matter。一篇新文章至少要有 `title`、`date` 和 `tags`：

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

- `title`：页面上显示的标题，可以用中文。
- `date`：建议写成带时区的时间，东八区用 `+0800`。只写 `2026-11-21` 也可以。
- `tags`：一个或多个标签。[标签]({{ "/tags/" | relative_url }})页会自动归类，标签名可以用中文。
- `layout`：可以省略。站点默认把 `_posts` 里的文章套上文章版式；写上 `layout: post` 更明确。

不想公开时，在 front matter 里加一行 `published: false`，或者把未写完的稿子放进 `_drafts` 目录（那里的文件不必带日期）。这两种都不会出现在网站上。

> 文件名里的日期会作为文章时间。如果 front matter 里另外写了 `date`，以 front matter 为准。

## 3. 写正文

front matter 下面用 Markdown 写正文。在希望首页摘要截断的地方单独放一行：

```html
<!-- more -->
```

这一行之前的文字会成为首页摘要。不写的话，摘要就是第一段。

图片可以放在 `assets/` 下，再用绝对路径引用，例如 `![一张图](/assets/images/note.png)`。

## 4. 推送到 main

提交后推送到 `main` 分支。仓库的 **Settings > Pages** 里，Source 选择 **Deploy from a branch**，分支选 **main**，文件夹选 **/ (root)**。

推送之后，GitHub Pages 会用它自带的 Jekyll 构建并更新 <https://stelfojia2023.github.io>。仓库里不需要、也不应再添加自定义 Actions 工作流。构建记录里可能会出现 GitHub 自带的 `pages-build-deployment`，那不是本仓库的文件。

本地想先看效果：

```bash
bundle install
bundle exec jekyll serve
```

然后打开 <http://127.0.0.1:4000>。只检查能否构建时，运行 `bundle exec jekyll build`，结果在 `_site/`。
