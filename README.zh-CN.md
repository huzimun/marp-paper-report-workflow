# Marp 论文汇报工作流

[English README](README.md)

`marp-paper-report-workflow` 是一个用于论文型 Marp/Markdown PPT 的 Codex skill。它的目标是把“基于多篇论文修改 PPT”变成可追溯、可复核、可版本管理的工作流：收集论文、生成中文简介、核查 PPT 表述、提取或标注论文图表、编译 PDF，并记录每轮修改。

## 开始前需要准备什么

建议为每个 PPT 新建一个独立项目文件夹。你可以把以下材料放进去：

- Marp/Markdown PPT，通常是 `.marp.md` 或 `.md`。
- 已下载好的论文 PDF。
- 论文标题、DOI、arXiv 编号、出版社链接或参考文献列表。
- 会议纪要或修改需求。
- 需要重点审批的事实、页码或图表要求。

也可以只提供 PPT 和论文名开始。如果 Codex 无法从出版社下载论文，应请求你提供本地 PDF；如果改用 arXiv 或其他公开仓库，必须核对标题、作者、年份、DOI 和版本是否一致。

## 推荐项目结构

skill 会在项目内创建或使用类似结构：

```text
project-folder/
├── deck.marp.md
├── workflow_outputs/
│   ├── papers/
│   ├── figures/
│   ├── artifacts/
│   ├── versions/
│   ├── paper_manifest.md
│   ├── paper_summaries.md
│   ├── fact_check_report.md
│   └── version_log.md
```

私有论文和 PPT 默认保留在本地项目文件夹中。除非你明确批准，不应上传到在线编辑器或外部服务。

## 标准使用流程

1. 新建独立项目文件夹，放入 PPT 和已有材料。
2. 要求 Codex 使用 `$marp-paper-report-workflow`。
3. Codex 识别 PPT、引用论文、图表占位符和缺失证据。
4. Codex 下载或整理 PDF，并核验论文身份。
5. Codex 生成 `paper_manifest.md` 和 `paper_summaries.md`。
6. Codex 将关键 PPT 表述追溯到论文原文，并记录人工可复核信息。
7. Codex 根据占位需求补图、裁剪、标注或重绘，并统一来源说明。
8. Codex 将 Marp Markdown 编译为 PDF，检查代表页面，并记录版本。
9. 用户审批事实、版式和最终输出。

## 功能清单

- 建立论文清单：标题、作者、期刊/会议、年份、DOI/arXiv、来源链接、本地 PDF、核验状态。
- 为每篇英文论文生成 150 到 300 字中文简介，帮助用户快速理解长 PDF。
- 将 PPT 关键表述追溯到论文摘录、PDF 页码、章节、图表或表格。
- 提取、裁剪、标注或简化论文图表，并保留来源信息。
- 使用 Marp 兼容的 HTML/CSS/SVG 绘制概念图。
- 将版本化 Marp Markdown 编译为 PDF。
- 维护版本日志，记录修改页码、命令、视觉检查、审批状态和未解决问题。

## 最终交付物

通常包括：

- 版本化 Marp Markdown。
- 版本化 PDF。
- `paper_manifest.md`
- `paper_summaries.md`
- `fact_check_report.md`
- `version_log.md`
- PPT 使用到的图像资产。

独立 HTML 通常不是交付物。HTML/CSS/SVG 可以作为 Marp Markdown 内部绘图方式。

## 版本管理规则

- 原始 PPT 作为 baseline。
- 不覆盖已确认版本。
- 每个正式版本使用 `deck.workflow-vNN.marp.md`，并生成同名 PDF。
- 正式历史放在 `workflow_outputs/versions/`。
- 当前候选稿和临时检查文件放在 `workflow_outputs/artifacts/`。
- 每轮正式修改都写入 `workflow_outputs/version_log.md`。

## 隐私与安全

- 不在公开记录中写入个人路径、用户名、凭据、cookie 或私有链接。
- 优先使用相对路径，例如 `workflow_outputs/papers/...`。
- 未经明确批准，不上传私有 PDF 或 PPT 到在线工具。
- 如果论文来自非出版社来源，必须先确认它与目标论文一致。

## 示例提示

```text
Use $marp-paper-report-workflow to fact-check and revise this paper-based Marp presentation with versioned outputs. Generate Chinese summaries for all papers, fill only pages with figure placeholders, compile a PDF, and record the version log.
```

## License

MIT License. See `LICENSE`.
