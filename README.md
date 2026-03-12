# paper-full-translate-zh

> 把论文 PDF 变成可读、可搜、可沉淀的中文研究资产，而不是一次性翻译垃圾。

![License](https://img.shields.io/badge/license-MIT-111111.svg)
![Skill](https://img.shields.io/badge/Copilot-Skill-0A66C2.svg)
![Output](https://img.shields.io/badge/output-2%20Markdown%20%2B%20Assets-0F766E.svg)
![Focus](https://img.shields.io/badge/focus-Full%20Paper%20Translation-9A3412.svg)

这是一个面向 VS Code Copilot Agent 的技能仓库。

它的目标不是“帮你总结一篇论文”，而是尽可能保真地完成这件事：

- 把整篇论文翻译成中文 Markdown
- 保留章节结构、图片、图题、表格、公式、附录、脚注、参考文献
- 同时生成一份真的有研究价值的 notes 文件
- 自动按论文标题建目录，把原论文和产物放在一起

最后你拿到的不是一段聊天记录，而是一套可继续使用的研究材料。

## 为什么这个项目值得 Star

大多数“论文翻译 Prompt”都会在几个地方翻车：

- 摘要认真翻，正文开始大幅省略
- 公式变量被改写，编号丢失，推导断裂
- 图题和表题消失，正文结构被揉碎
- appendix、脚注、致谢、参考文献被静默跳过
- 最终结果像是摘要扩写，不像全文翻译

paper-full-translate-zh 反过来做：

- 它优先保证结构完整，而不是先追求表面流畅
- 它允许降级，但不允许静默丢失
- 它输出的是目录化研究资产，不是一次性对话回复
- 它把“剥洋葱式文献导读”放到 notes.md 开头，帮助先抓住主线再回读正文

如果你平时读论文、做组会、写笔记、沉淀知识库，这个 skill 解决的是很具体、很高频、很痛的那部分工作。

## 一眼看懂它产出什么

默认情况下，skill 会先创建一个以论文标题命名的目录，再把原论文和产物统一放进去：

```text
<paper_title_dir>/
  <original_paper_filename>.pdf
  <paper_stem>.zh-CN.full.md
  <paper_stem>.zh-CN.notes.md
  <paper_stem>.assets/
```

真实效果应该接近这样：

```text
ThinkRec - Thinking-based recommendation via LLM/
  Yu et al. - 2026 - ThinkRec Thinking-based recommendation via LLM.pdf
  ThinkRec - Thinking-based recommendation via LLM.zh-CN.full.md
  ThinkRec - Thinking-based recommendation via LLM.zh-CN.notes.md
  ThinkRec - Thinking-based recommendation via LLM.assets/
    figure-01.png
    figure-02.png
```

其中：

- full.md：全文保真翻译，负责把正文重建完整
- notes.md：开头先放剥洋葱式文献导读，后面接研究笔记
- 原论文：直接放在同目录，避免原文和产物散落
- assets：保存正文图片，以及无法稳定重建时的图表资源片段

默认会导出图片文件，并在 full.md 中使用相对路径引用这些图片。
图像信息通过图片本体、图号、图题和必要的上下文一起保留下来，公式优先保留为 LaTeX，复杂表格优先重建为 Markdown 或 HTML。

## 这不是普通 Prompt，而是一个研究工作流

| 维度 | 普通论文翻译 Prompt | paper-full-translate-zh |
| --- | --- | --- |
| 目标 | 生成一份看起来像译文的内容 | 重建一份可追溯的全文中文 Markdown |
| 结构 | 经常打散章节、图片和附录 | 显式保留主结构、图片、图题、表格、附录 |
| 公式 | 容易改变量名或直接丢失 | 优先保留 LaTeX、编号和上下文 |
| 失败处理 | 常常静默省略 | 明确标记提取风险和降级位置 |
| 结果形态 | 一次性聊天输出 | 可归档、可检索、可继续编辑的研究资产 |
| 阅读辅助 | 需要你再额外追问总结 | notes.md 自带剥洋葱式导读和研究笔记 |

## 核心能力

### 1. 全文级保真翻译

- 面向整篇论文，而不是只面向摘要或正文前几节
- 不默认跳过 appendix、footnote、acknowledgement、references
- 公式前后的解释文字会翻译，公式本体尽量保持原始形式

### 2. 结构化重建，而不是纯文本搬运

- 保留章节层级
- 保留图片、图号和图题
- 表格优先还原为 Markdown 或 HTML
- 引用、脚注、附录尽量放回正确位置

### 3. 剥洋葱式文献导读

notes.md 开头固定包含四步导读：

1. Context：一句话说清这篇论文到底在解决什么实际问题
2. Grounding：用生活隐喻把核心机制讲明白
3. Core Focus：只拆 1 到 2 个真正关键的核心公式
4. Exhaustive Mapping：再把剩余推导和边缘定义补回主线

这不是为了写得花，而是为了降低论文阅读门槛。
你先拿到直觉，再回去啃正文和公式，效率会高很多。

### 4. 目录化归档

- 自动按论文标题建立目录
- 本地 PDF 会被剪切到目标目录中
- 全文译文和笔记天然与原文同目录

这一步很朴素，但对长期积累最重要。

## 适合谁

- 需要系统读论文的研究生、博士生、工程师
- 想把论文沉淀到 Obsidian、Markdown 知识库的人
- 做推荐系统、LLM、NLP、CV 等领域文献追踪的人
- 需要在组会前快速整理出可用材料的人
- 想把“读论文”从聊天记录升级成工作流的人

## 快速开始

### 1. 安装到技能目录

把这个仓库放到你的技能目录：

```text
.agents/skills/paper-full-translate-zh/
  SKILL.md
  README.md
```

### 2. 在 VS Code Copilot Agent 中直接调用

你可以直接说：

```text
把这篇 PDF 全文翻译成中文 Markdown，保留图片、公式和图题，并在同目录生成阅读笔记。
```

```text
处理这个 arXiv 论文链接，输出中文全文 md 和一份 notes 文件，放到论文名称命名目录里，并导出图片 assets。
```

```text
对这篇论文做逐段翻译，不要省略 appendix，公式用 LaTeX，图片和图题尽量原位保留。
```

```text
对这篇论文做全文翻译，并在 notes.md 最前面追加剥洋葱式文献导读，总共还是只输出两个 md。
```

```text
把这篇 PDF 剪切到一个以论文名命名的目录里，再输出全文翻译和 notes，所有文件都放在这个目录中。
```

## 它背后的默认处理原则

这个 skill 不是胡乱拼接，它有明确的优先级：

```text
结构化 HTML / LaTeX > 可提取文本的 PDF > OCR PDF
```

执行时会优先做这些事：

1. 确认论文来源和标题
2. 创建以论文标题命名的目录
3. 先建立结构映射，再逐段翻译
4. 重建章节、图片、图题、表格、公式和参考文献
5. 生成 notes.md，并把剥洋葱式导读放在最前面

它的设计哲学很简单：

1. 宁可显式降级，也不静默省略
2. 宁可保留原词，也不乱编术语
3. 先保证结构完整，再优化语言顺滑
4. 全文翻译不是摘要扩写
5. 笔记必须服务研究判断，而不是重复正文

## 什么算是一个合格输出

一个靠谱结果，至少应该满足：

- 可以从头到尾顺序阅读，不频繁跳失上下文
- 原论文、full.md、notes.md、assets 位于同一个论文目录
- 主结构与原文一致，章节层级清楚
- 图片、图题、表格、公式出现在大致正确的位置
- appendix、caption、footnote、acknowledgement、references 不被默认漏掉
- notes.md 开头包含完整四步剥洋葱式导读
- 提取不稳的地方有明确标注，而不是假装翻好了

## notes.md 为什么是这个项目的灵魂部分

很多工具能翻译，但很少有工具能让你真正更快读懂论文。

这个项目把 notes.md 单独拉出来，并且固定做两件事：

- 先帮你建立理解主线
- 再帮你形成研究判断

通常 notes.md 会包含：

- 论文基本信息
- 一句话核心问题
- 方法主线
- 主要贡献
- 关键实验结论
- 关键公式或机制
- 优点与局限
- 与当前研究主题的关系
- 值得继续追的问题

这意味着你不只是获得了译文，还获得了一份可复用的研究阅读入口。

## 适用输入

- PDF
- arXiv 页面
- 普通 HTML 论文页
- LaTeX 源码
- 扫描版 PDF（允许 OCR 降级，但会标注风险）

## Roadmap

- 更稳定的多栏 PDF 重排
- 更强的复杂表格还原
- 更细粒度的图题与公式回溯标记
- 批量处理多篇论文的工作流模板
- 面向不同学科的术语风格配置

## 贡献方向

欢迎围绕这些方向提交 issue 或 PR：

- 真实论文样例和失败案例
- 复杂表格、附录、脚注场景的修复策略
- 更好的 Markdown 重建规则
- 面向不同学科的提示模板
- 与 Obsidian、知识库、笔记系统的集成方式

## 如果这个项目对你有用

如果你认同下面任意一句，这个项目大概率值得你点个 Star：

- 我想要的不是摘要，而是能留下来的研究资产
- 我不想再花时间手工整理 PDF、笔记和正文
- 我希望翻译后的论文以后还能搜、还能改、还能引用
- 我想先快速读懂论文主线，再决定要不要深挖复现

它不是万能的，但它解决的是研究工作流里最容易反复消耗人的那一段。

## License

MIT