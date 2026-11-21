# 栏目发布步骤

本文是本仓库的「Sites 技能」。每天四栏文章按这里写、合并、核对。计划原文在 `docs/DAILY-PLAN.md`，执行时以该文件开头的「本站适配说明」为准。

发布目标是 <https://stelfojia2023.github.io>。部署就是把当天的拉取请求合并进 `main`，GitHub Pages 从 `main` 根目录重新构建。不要添加自定义 Actions，也不要改站点权限。

进度只看本仓库的 `article-log.json`。未在本站核验上线之前，不要改 `cursors`。

## 四栏

| category | 栏目 | 栏目页 | 首页锚点 |
| --- | --- | --- | --- |
| `ai` | AI 工程图解 | `/ai/` | `#ai` |
| `tongjian` | 通鉴今读 | `/tongjian/` | `#tongjian` |
| `agama` | 阿含日课 | `/agama/` | `#agama` |
| `matt` | Matt 技能课 | `/matt/` | `#matt` |

首页和栏目页里，文章列表由 Jekyll 按 `category` 生成，包在 `<!-- articles:<category>:start -->` 与 `<!-- articles:<category>:end -->` 之间。日更不要往标记中间手写链接。写上对应的 `category`，构建后会自动出现在标记里。

## 当天接续点

先读 `article-log.json` 的 `cursors`，再写文章。

- `ai`：`next` 为 `null`，表示还没有读过。每天另选一篇尚未出现在 `entries` 里的 OpenAI 或 Anthropic 官方技术文章。
- `tongjian`：从 `next_start`「初，智宣子將以瑤為後」接，不要重写旧站已刊的首篇。
- `agama`：从 `next_start`「T02n0099 第2经 p.1a16–27」接，不要重写第 1 经。
- `matt`：下一课是 `series_order` 2，`skill_slug` 为 `ask-matt`，来源 <https://www.aihero.dev/skills-ask-matt>。第 1 课 `matt-001-setup` 只在旧站，本站不转载。

某栏缺原典或没通过核验时，先合并已通过的篇目。不要为了跳过而把游标移过未发的那一段。

## 1. 新建文件

每天每栏一篇，放在 `_posts`。文件名：

```text
_posts/YYYY-MM-DD-<category>-<slug>.md
```

例如 `_posts/2026-11-22-matt-ask-matt.md`。日期用北京时间。`<slug>` 用英文短横线，不要写中文。站点固定链接是 `/:year/:month/:day/:title/`，所以上例的线上地址是：

```text
https://stelfojia2023.github.io/2026/11/22/matt-ask-matt/
```

## 2. 文首信息

```yaml
---
layout: post
title: 文章标题
date: 2026-11-22 08:00:00 +0800
category: matt
tags:
  - Matt 技能课
# 可选。文章自有样式必须写成列表，会排在 article-theme.css 之前。
extra_css:
  - /assets/css/某篇自有.css
---
```

`category` 只能是 `ai`、`tongjian`、`agama`、`matt`。不要把样式写进正文里的 `<style>`，否则会排到 `assets/article-theme.css` 后面，盖住共用样式。

共用样式已在文章版式里引入，路径是 `/assets/article-theme.css`。

## 3. 各栏正文顺序

二级标题用下面的文字和 `id`，不要调换顺序。目录和正文一致。

### AI 工程图解（`ai`）

1. `## 问题与为什么值得读`，`id="why"`。先写全文要解决什么、为什么值得读。注明标题、作者或团队、日期、官方原文链接。
2. `## 按原文顺序拆解`，`id="reading"`。按原文顺序写观点、机制、适用条件和限制。保留关键条件、数字、术语和结论。术语第一次出现就用中文讲清。分开原文观点、自己的解释、类比和未验证的推断。
3. `## 图解`，`id="figure"`。用结构图、流程图或示意图解释一处关键关系。图放在 `<figure class="diagram">` 里，`<figcaption>` 写清是原创还是来源。不能合法使用的原图就链接原图。
4. `## 对工程实践的意义`，`id="practice"`。写对 AI 技术演进或工程实践的具体意义。适合时加一个标明的 ESP32/OCPP 或 Agent 例子。

未由用户提供全文时，只做忠实的详细转述和允许范围内的短摘译，不逐段完整翻译。

### Matt 技能课（`matt`）

1. `## 英文原文`，`id="original"`。署名。列出官方页面，需要时列出官方 `SKILL.md`。未允许全文转载时，每个来源最多摘 25 个英文词。
2. `## 中文翻译与讲解`，`id="explain"`。先译短摘，再说明不用它会卡在哪里。用 3 到 6 步写输入、谁来做、为什么得到这个结果。术语用普通话在第一次出现时定义，并写一个容易混淆之处和何时不用。更深的细节放进 `<details>`。
3. `## 示例`，`id="example"`。一个贯穿的 ESP32/OCPP 或 Agent 场景：环境、在哪操作、怎么调用、粘贴什么、会看到什么、哪一步停下。至少一段回显，标成模拟或实测。给一个常见出错点和可观察的过关标准。写入、远端或设备操作前用 `<p class="stop">` 标出停点。例子默认只读或模拟。不要把示例说成已在用户机器上实测。

### 通鉴今读（`tongjian`）

顺序固定：白话、议古论今、原文。

1. `## 白话文`，`id="vernacular"`。逐段自译，不用摘要代替翻译。
2. `## 议古论今`，`id="present"`。先问一个具体问题。用一件可核实的当代事件对照，并给出处。没有合适事件时写明本篇不做今例。结尾留一个能具体回答的问题。
3. `## 原文`，`id="source"`。保留选定范围的完整原典。底本、异文和下篇接续写在这一节里。标卷次、能确定的纪年、原文起止和可定位来源。

### 阿含日课（`agama`）

顺序固定：白话、经义与今用、经文原文。

1. `## 白话文`，`id="vernacular"`。说清这经讲了什么。逐段自译。
2. `## 经义与今用`，`id="present"`。只拆一条核心道理：这句话是什么意思、前后怎么连、它不等于什么。分开经文本意、注明出处的传统解释和今天的应用。用可核实的事件对照，另给一项日常短练习，并留一个能凭自己的观察回答的问题。练习不是经文，也不作医疗建议。
3. `## 经文原文`，`id="source"`。完整保留本篇范围的经文。注明经号、卷次、页栏行和原典链接，以及下一天从哪里接。

白话和原文按同一序号双向跳转。第 1 段白话链到第 1 段原文，原文再链回来。不要把另一版本或后人注混进正文。

```html
<p class="para" id="v-1">
  <a class="para-num" href="#v-1">1</a>
  白话这一段。
  <a class="jump" href="#o-1">原文</a>
</p>
```

```html
<p class="para para-source" id="o-1">
  <a class="para-num" href="#o-1">1</a>
  原文这一段。
  <a class="jump" href="#v-1">白话</a>
</p>
```

段号从 1 连续增加。`v-N` 与 `o-N` 必须成对。

## 4. 更新 article-log.json

每篇在 `entries` 追加一项。刚写进拉取请求、尚未在线上看到时，`published` 必须是 `false`。这时不要修改 `cursors`。

各栏都有的字段：`date`、`category`、`title`、`url`、`source`、`published`。

通鉴和阿含再写 `read_until`、`next_start`。AI 与 Matt 这两项用 `null`。

Matt 再写 `series_order`、`skill_slug`、`next_cursor`。其他栏这两项不要填，或显式用 `null`。

`url` 用上面的绝对地址。字段说明也写在 `article-log.json` 的 `entry_schema` 里。

## 5. 合并前检查

在拉取请求里确认：

- 文件名、`category` 和三节或四节的顺序与上文一致。
- 来源链接能打开。通鉴、阿含的白话段号和原文段号一一对应。
- 当代事件写了时间和出处；有争议时写明是谁的说法。
- 图和正文说的是同一件事，图注标明原创或来源。
- 首页四个锚点、栏目页和导航还在。标记仍是 `<!-- articles:ai:start -->` 这种形式，中间仍是生成的列表。
- 窄屏下段落号、跳转链接、折叠块和图片不横溢。没有在手机宽度看过，就不要在汇报里说已经验证移动端。
- 本地执行 `bundle exec jekyll build`，构建没有错误。
- 本栏若未通过，就不要把它算进这次合并，也不要推进它的游标。

不要在日更里改首页设计、导航或 `assets/article-theme.css`。2026-11-21 这次改版改过首页和文章版式，是单独的外观调整。`<!-- articles:<category>:start -->` 与 `<!-- articles:<category>:end -->` 的写法没有变，列表仍由 `category` 生成。此后的日更不要再改这套外观。

## 6. 合并之后核对线上地址

合并进 `main` 后，等 GitHub Pages 的 `pages-build-deployment` 完成，再逐篇打开：

- 文章：`https://stelfojia2023.github.io/YYYY/MM/DD/<category>-<slug>/`
- 栏目页：`https://stelfojia2023.github.io/ai/`、`/tongjian/`、`/agama/`、`/matt/`
- 首页锚点：`https://stelfojia2023.github.io/#ai`、`#tongjian`、`#agama`、`#matt`
- 日志：`https://stelfojia2023.github.io/article-log.json`

页面返回成功，并且标题出现在栏目页和对应首页锚点下，才把该条 `published` 改成 `true`。同时更新这一栏的 `cursors`：

- 通鉴、阿含：`read_until` 写成这篇实际读完的位置，`next` 和 `next_start` 写成下一篇起点。
- Matt：`series_order`、`skill_slug`、`next`、`next_cursor` 改成下一课。下一课按 AI Hero 官方目录顺序，不按发布时间。
- AI：没有连载游标。`cursors.ai.next` 保持 `null`。已读记录只留在 `entries`。

这一次改动可以是合并后的小提交。线上没看到文章，就不要把 `published` 写成 `true`，也不要移动 `cursors`。

汇报用一条中文消息发到站主的 Grok Bot 对话，只列实际已上线的标题和链接。没上线的栏要写明缺哪一栏、原因，以及已经核实、可以交付的内容。
