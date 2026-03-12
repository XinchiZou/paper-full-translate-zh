# OneRec Example

这是一个面向公开 skill 仓库的仓库安全示例，用来展示 paper-full-translate-zh 在真实论文上的预期输出形态。

## 对应论文

- 标题：OneRec: Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment
- 作者：Jiaxin Deng 等
- 年份：2025
- 场景：工业级生成式推荐，统一检索与排序，并使用 Iterative Preference Alignment 做偏好对齐

## 本地实例的目标目录结构

在本地工作区里，这个案例的完整输出目录会是：

```text
OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment/
  Deng 等 - 2025 - OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.pdf
  OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.zh-CN.full.md
  OneRec Unifying Retrieve and Rank with Generative Recommender and Iterative Preference Alignment.zh-CN.notes.md
  assets/
    figure-01.png
    figure-02.png
    ...
```

## 这个实例主要说明什么

1. skill 会把原论文、全文翻译、阅读笔记和资源目录统一收纳到同一个论文目录中。
2. full.md 负责结构保真的全文重建；notes.md 则把剥洋葱式文献导读放在最前面。
3. 图片和复杂表格会优先以 assets 中的相对路径资源保留，避免正文结构丢失。
4. 资源目录固定使用短名称 assets，以降低 Windows 下的路径长度风险。

## 为什么这个示例没有直接附带 PDF 与完整产物

这个 skill 仓库是公开仓库。为了避免直接重新分发原论文 PDF、整篇译文和论文图表资源带来的版权风险，这里只保留案例说明，而不直接提交完整论文文件与导出资源。

如果你在自己的本地工作区运行该 skill，仍然会得到完整的论文目录和全部产物。