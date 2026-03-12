# OneRec Example

这是一个真实实例目录，用来展示 paper-full-translate-zh 在一篇完整论文上的实际输出结果。

## 对应论文

- 标题：OneRec: Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment
- 作者：Jiaxin Deng 等
- 年份：2025
- 场景：工业级生成式推荐，统一检索与排序，并使用 Iterative Preference Alignment 做偏好对齐

## 当前目录结构

当前示例目录已经包含完整产物：

```text
OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment/
  Deng 等 - 2025 - OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.pdf
  OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.zh-CN.full.md
  OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.zh-CN.notes.md
  assets/
  README.md
```

## 这个实例包含什么

1. 原论文 PDF：保留在同目录下，便于随时对照原文核查。
2. 全文翻译：full.md 负责结构保真的中文重建，尽量保留章节、图题、表格、公式和参考文献。
3. 阅读笔记：notes.md 在最前面包含“剥洋葱式文献导读”，后面补充研究视角下的方法主线、实验结论、优点、局限和后续问题。
4. 资源目录：assets 统一保存图片和复杂图表片段，Markdown 通过相对路径直接引用。

## 这个实例主要说明什么

1. skill 的交付目标不是一段聊天式摘要，而是一套可以继续阅读、检索和沉淀的论文目录。
2. 原论文、全文翻译、笔记和资源文件会被统一收纳到同一个论文名称目录中。
3. 资源目录固定使用短名称 assets，这样在 Windows 下更稳，能减少路径过长导致的预览或复制问题。
4. notes.md 不只是摘要复述，而是面向研究阅读的辅助入口，帮助先抓主线，再回到全文和公式。

## 建议阅读顺序

1. 先看 notes.md 开头的剥洋葱式文献导读，快速抓住问题、隐喻和核心公式。
2. 再看 notes.md 后半部分的研究笔记，判断这篇论文的方法价值和局限。
3. 最后回到 full.md 顺序阅读正文，并结合 PDF 与 assets 交叉核对图表和公式细节。

## 为什么保留这个实例

这个目录可以直接作为 skill 的输出参考样例：

- 如果你想看一个完整论文目录最终会长成什么样，可以直接看这个实例。
- 如果你想检查 full.md、notes.md 和 assets 之间的组织关系，这个实例也是最直接的对照。
- 如果你想扩展或修改 skill 的规则，它还能作为真实回归样例，帮助判断改动有没有破坏最终产物形态。