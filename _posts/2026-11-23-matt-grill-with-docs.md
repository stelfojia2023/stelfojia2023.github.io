---
layout: post
title: 第3课：词一定下来，就写进词汇表
date: 2026-11-23 08:03:00 +0800
category: matt
tags:
  - Matt 技能课
---

grill-with-docs 用来追问一个还没说清的计划。一个词定下来，它就写进仓库里的词汇表，而不是等谈话结束再一起写。它不替你写规格，也不改固件。

<!-- more -->

<nav class="toc" aria-label="目录">
  <ol>
    <li><a href="#original">英文原文</a></li>
    <li><a href="#explain">中文翻译与讲解</a></li>
    <li><a href="#example">示例</a></li>
  </ol>
</nav>

## 英文原文
{: #original}

这一课讲 Matt Pocock 的技能 `grill-with-docs`。官方说明页是 <https://www.aihero.dev/skills-grill-with-docs>。官方技能文件是 <https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md>。本课是本站的第 3 课。上一课是 ask-matt。

未获准全文转载。每个来源只摘不超过 25 个英文词，其余用我的话说明。

说明页的短摘：

> When a term resolves, the skill writes it to GLOSSARY.md at once, not in a batch at the end.

技能文件的短摘：

> Call the Skill tool twice, for "grilling" and "domain-modeling".

仓库 README 里和客户端有关的安装行，一共十三个英文词，列在下一节，不在这里加长摘录。见 <https://github.com/mattpocock/skills/blob/main/README.md>。

官方顺序我按说明页上的主链核对，不按发布时间。说明页把这条链写成：grill-with-docs，然后 to-spec，然后 to-tickets，然后 implement，然后 code-review，然后 retro。to-spec 的说明页今天仍在 <https://www.aihero.dev/skills-to-spec>，并写明 `/to-prd` 已在 v1.1 改名为 `/to-spec`，旧的短名不再可用。技能总览页的推荐名单里还看得到 `/to-prd` 这几个旧名字。那份推荐名单和这条主链不一致时，本课跟主链，下一课仍是 to-spec。这和已经约定的早期顺序没有冲突，本课不改道，也不暂停。

## 中文翻译与讲解
{: #explain}

先译短摘。说明页那句的意思是：一个词一旦定下来，技能就立刻把它写进 `GLOSSARY.md`，不是等到最后成批写入。技能文件那句的意思是：去调用两次技能工具，一次给 grilling，一次给 domain-modeling。

作者的说法是：这和 grill-me 是同一场追问，只是对准一个代码仓库。追问的节奏是一轮问题，然后等你，然后再一轮。它是有状态的。别的追问把结果留在你脑子里。这一项会在磁盘上留下文件。词写进词汇表。一项决定若同时通过三道门，才写成一份架构决策记录，文件放在 `docs/adr/`。我的理解：把它当成「边问边落笔的对齐」，不要把它当成「把今天聊过的话全部归档」。

不用它，会卡在这里：你已经在一个仓库里，计划还模糊，事情用什么词都还没定。代理若直接去改代码，就会按它猜的那个词动手。上一课的路由器只负责点名。点完名若不停下来问，词还是没有定。说明页认为，这种时候该在一次会话里追问，并把定下来的词写进仓库。

按说明页上的用法，做这五步：

1. 你自己输入 `/grill-with-docs`。说明页写明，要由你来调用，代理不会自己去拿它。输入是还没说清的计划，不是一份已经写好的规格。
2. 它一轮一轮地问，并等你答。仓库里已经写明的事，它该自己去读，不拿来问你。
3. 一个词定下来，它立刻写入 `GLOSSARY.md`。根目录一份；若根上有 `GLOSSARY-MAP.md`，标明仓库分成多块上下文，就写到对应那一块的词汇表。文件在第一次需要时才创建。你不用事先建空文件。
4. 一项决定要同时满足三道门，才另写架构决策记录：难撤回、没有上下文会让人吃惊、并且是真正的取舍。三道都过，才写。多数决定写不进去。一次会话只有更清楚的词汇表、没有决策记录，说明页认为这是正常的。
5. 其余定下来的事只留在这次对话里。说明页要你把这次对话交给 to-spec，而不是清掉。本课停在追问和词汇。to-spec 是下一课，这里不跑。

术语。词汇表，是这个项目自己的词和紧的定义，不是规格，也不写实现细节。架构决策记录，是一份短文件，只留给那种以后再吵会很痛的决定。上下文，是这一次对话里模型还能看见的文字。一轮，是问完就停，等你答，不是把所有问题一次倒出来。这些是我用普通话给说明页里的词做的定义。

容易混淆的一点：`grill-with-docs` 和 `grill-me`。两者都是追问。前者在仓库里，并且写文件。后者不在工作目录里用，也不留文件。另一处容易混的是它和 `domain-modeling`。后者是它拿来写词汇表和决策记录的那一项纪律。技能文件本身几乎只有一句委托。只装了 grill-with-docs、没有把 grilling 和 domain-modeling 也装上，说明页认为你得到的是一个不能工作的技能。

什么时候不用。第一，你根本不在一个工作目录里。用 grill-me。第二，这件事一次会话装不下，例如一块新系统或很大的功能。说明页把这种情况指到 wayfinder，并按会话次数来分：一次会话用本课，多次会话用 wayfinder。第三，事情已经定了，而且一次上下文窗口就做得完。说明页说可以直接去 implement，规格那一步可以跳过。第四，决定卡在别人脑子里。说明页指到 to-questionnaire，让那个人异步或当面填。第五，你其实想让它开始改产品代码。写词汇表是它的输出。改固件不是。

客户端的写法要分开。Claude Code 用斜杠，官方说明页写的调用就是输入 `/grill-with-docs`。Codex 在仓库 README 里的安装是另一组命令，先 `codex plugin marketplace add mattpocock/skills`，再 `codex plugin add mattpocock-skills@mattpocock`。Claude Code 的安装行是 `claude plugin install mattpocock-skills@claude-plugins-official`。说明页没有另外写出一套 Codex 选择器的点选步骤。所以下面的示例只演示已经写明的斜杠，不把某种我没有在这页上看到的选择器说法，写成官方命令。这些安装行来自 README，不是本课要你现在去执行的步骤。

<details>
  <summary>三道门、词汇表给谁用，以及两个作者已经写明的故障</summary>
  <p>说明页把一次会话的结果分成三等。词，立刻进词汇表。又难撤回、又会让外人吃惊、又是真正取舍的决定，才进 <code>docs/adr/</code>。其他你已经定了的事，只存在于这次对话。第三等最容易让人以为「已经写进仓库了」。没有。词汇表不记实现，不记规格，不记草稿。多数会话因此一份决策记录都没有。说明页说，这意味着你们刚同意的大部分内容，只活在同意它的那个上下文里。要留下，就把同一次对话交给 to-spec。清掉再写，那些精确的答案会被后面的步骤说软。</p>
  <p>词汇表的用处，说明页没有写成已证实的模型加速。它转述了最强的反对：一个词和它的白话解释，模型给出的结果可以一样；词汇主要是缩短已经共享这套词的人之间的说话。按这个反对，词汇表仍然有用，但用处在人。作者没有在这页上用数字驳回这个反对。我也不补数字。</p>
  <p>说明页写了两个还在的问题。一个是：技能若被另一层编排包起来调用，例如某个规格流程、多智能体框架，或别人管道里的一步，使用者报告追问还在，写文件的那一半会静默不发生。问题已记录，尚未修好。另一个是：依赖没装上时，代理会一次问完，不给建议，也不提词汇表。若只装上 grilling、没装上 domain-modeling，你会得到一场像样的追问，却没有纸面记录。说明页说这是这项技能被报告得最多的问题。怀疑时，直接问代理它加载了哪几项技能。</p>
</details>

## 示例
{: #example}

贯穿场景仍是上一课那台 ESP32 充电桩固件。你懂 OCPP 1.6。你不懂这些技能。上一课的路由器已经停住，并让你自己敲下一项。眼下的卡点是：「打开」还没有定义。它可能指接触器吸合，也可能指连接器锁止。词不定，代理就会猜一个引脚去改。

不用 grill-with-docs 时，你会说「按你的理解实现」。代理选定一个意思，开始改 `main.cpp`。仓库里仍然没有一句写明「打开」指什么。下一次会话会再猜一次。这就是这一课要挡住的地方。

环境和前提：一个已经有固件仓库的目录，技能按作者的安装说明装好，并且 grilling 和 domain-modeling 也在。本示例不要求你现在安装。你在对话里操作，不在桩上操作。下面全部是模拟，不是在你的机器上、也不是在 WSL 里实测过的记录。

在哪里操作：Claude Code 的对话输入框。怎么调用：输入斜杠 `/grill-with-docs`，然后把下面这段粘贴进去。Codex 的官方安装命令见上一节；本页没有给出选择器里要点哪一项，所以这里不演示点选。

粘贴的输入：

<pre class="echo"><code>I am in an ESP32 firmware repo for an OCPP 1.6 charger.
I want a StatusNotification when the relay opens.
I have not decided whether "open" means the contactor or the connector lock.
Interview me. Read the repo before you ask what the code already says.
Do not edit firmware. Do not write GLOSSARY.md until I answer.</code></pre>

按说明页，它不该把所有分支一次问完。模拟的第一轮只问一个词，并说明代码里还没有这个定义。你的回答是：在这个仓库里，「打开」指接触器吸合，不指连接器锁止。这个词由此定下来。

模拟回显，不是实测：

<pre class="echo"><code>Round 1. The firmware I can read never defines "open".
Does "open" mean the contactor closes, or the connector lock releases?
I will wait. I will not edit files before you answer.</code></pre>

你回答以后，说明页要求的下一步是立刻写词汇表，而不是再聊十轮。模拟中将要写入的那几行是：

<pre class="echo"><code>GLOSSARY.md
Open: the contactor closes. It does not mean the connector lock releases.</code></pre>

<p class="stop">停在写入之前。本课的过关不保存这个文件，不创建 <code>docs/adr/</code>，不修改源文件，不写 platformio.ini，不编译，不给充电桩刷写，也不连接桩的串口。若你以后在自己的仓库里让它真的写词汇表，先确认这个目录允许写入。写固件、刷桩、改继电器，仍不是这一课的输出。</p>

这一问没有架构决策记录。它只定了一个词。说明页的三道门要同时成立。这里没有一项「难撤回、外人会吃惊、又是真正取舍」的设计决定需要另写文件。没有决策记录，是说明页所说的正常结果。

会看到什么：一轮一个问题，你回答后它给出将写入词汇表的那一句，然后停。它不开始 `/to-spec`，也不改固件。你以后可以自己敲 `/to-spec`。那是下一课的事。

常见出错：它一次抛出十个问题，并且全程不提 `GLOSSARY.md`。说明页把这写成依赖没有加载：技能文件只是一句委托，代理若没读到 grilling 和 domain-modeling，就会自己猜「追问」是什么。另一个常见出错，是追问进行了，工作区里却没有任何文件。先分清两种原因。一种是本来就没有可写的词或决定。一种是它跑在别的编排层里面，写文件的一半会静默不做。处理是问它加载了哪几项技能，并在相信输出之前看一眼工作目录。不要顺着它去改固件。

自检：看工作区有没有新的改动。这一课若保持模拟，应该没有。词汇表那一行里没有引脚号，也没有寄存器地址。

过关标准：你能复述「它一轮一轮问；词一定下来就该写入词汇表；规格和固件都不是它的输出」。你能指出这次为什么不写架构决策记录。仓库里没有被这次问答改动的文件。你还没有给桩上电，也没有刷写。
