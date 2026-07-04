# Marp 论文汇报工作流

`marp-paper-report-workflow` 是一个用于论文型 Marp/Markdown 课件的 Codex skill。它现在分为两个模式：

- **快速填图模式**：用户已经提供图像、表格截图或裁剪图时使用。Codex 只负责放入指定 PPT 页、写合适的中文说明、补来源脚注、导出 PDF 并做视觉检查。
- **完整论文审校模式**：需要下载论文、整理 PDF、从论文中抓图、事实核查、生成论文中文摘要或全稿审校时使用。

核心原则是：先选择满足需求的最轻流程，避免把局部填图任务扩大成完整论文审计。

## 你需要准备什么

建议每个课件建立一个独立项目文件夹，并放入已有材料：

- Marp/Markdown 课件，最好是 `.marp.md` 或 `.md`。
- 如果只是快速填图，提供图像、表格截图或裁剪图。
- 如果要完整审校或抓图，提供论文 PDF 或论文标题、DOI、arXiv、出版社链接等。
- 会议纪要、页面修改要求、需要人工确认的事实边界。
- 明确的审批要求，例如只改哪些页、编译 PDF 后是否暂停。

如果你已经提供图片，Codex 应默认使用快速填图模式，不应为了重复获取同一张图而下载论文或反向抓 PDF。

## 推荐项目结构

```text
project-folder/
├── deck.marp.md
└── workflow_outputs/
    ├── papers/
    ├── figures/
    ├── artifacts/
    ├── versions/
    ├── paper_manifest.md
    ├── paper_summaries.md
    ├── fact_check_report.md
    └── version_log.md
```

快速填图模式通常只会更新 `figures/`、`artifacts/`、`versions/` 和 `version_log.md`。完整论文审校模式才会更新 `papers/`、`paper_manifest.md`、`paper_summaries.md` 和 `fact_check_report.md`。

## 快速填图模式

适用于这些请求：

- “图片我已经给你了，填到第 57、66、67 页。”
- “根据图表标题、用途和截图建议写中文说明。”
- “尽快让我看到填充后的 PDF，编译完先暂停。”
- “调整这几页图像大小、位置、说明和来源脚注。”

流程：

1. Codex 识别最新可用基线版本，并创建下一版工作稿。
2. 读取指定页的 `图表占位`、`用途`、`截图建议` 和周围教学点。
3. 直接使用用户提供的图片或表格资产。
4. 用 Marp 布局放入图片，不默认改动图片像素。
5. 写独立可读的中文说明，开头使用 `Author et al. Fig. X:` 或 `Author et al. Table X:`。
6. 在底部补统一来源格式：`来源：Author et al., Paper Title, Venue, Year, https://...`
7. 导出 PDF，检查指定页边界、字号、图片清晰度、说明是否越界。
8. 写简短版本日志，并在用户要求时暂停等待检查。

快速模式默认不做：

- 下载论文；
- 从 PDF 抓图；
- 重建完整论文清单；
- 给每篇论文写中文摘要；
- 全稿逐页事实核查；
- 运行与当前修改无关的 workflow validation 样例。

示例 prompt：

```text
使用 $marp-paper-report-workflow 的快速填图模式。图片我已经给出，请填充第 57、66、67 页，根据占位说明写合适中文说明，导出 PDF 后先暂停让我检查。
```

## 完整论文审校模式

适用于这些请求：

- “请下载/整理这些论文 PDF。”
- “从论文中提取 Fig. 1 / Table 1 并填入 PPT。”
- “事实核查整份课件，防止幻觉。”
- “生成论文中文摘要、manifest、fact-check record。”
- “验证完整自动化工作流。”

流程：

1. 识别课件、引用论文、占位页和缺失证据。
2. 下载或整理论文 PDF，并核对标题、作者、年份、DOI/arXiv 和版本。
3. 建立 `paper_manifest.md`。
4. 为论文生成 150-300 字中文摘要，写入 `paper_summaries.md`。
5. 对用户批准范围内的关键陈述做事实核查，记录可人工复核的位置和摘录。
6. 从论文原图中提取、裁剪、标注或重绘图表。
7. 编译 PDF，检查代表页，写入版本日志和审校记录。

示例 prompt：

```text
使用 $marp-paper-report-workflow 的完整论文审校模式，下载并核对课件中的论文，事实核查关键页面，补齐缺失图表，导出 PDF，并记录版本日志。
```

## 版本规则

- 原始课件作为 baseline，不直接覆盖。
- 每一轮正式修改创建 `deck.workflow-vNN.marp.md` 和对应 PDF。
- 已批准版本不可覆盖；需要修正时创建下一版本。
- 如果用户说“删除/重做某版本”，正式版本应在日志中标为 `rejected`、`deprecated` 或 `superseded`，而不是静默删除历史。
- `versions/` 保存正式历史，`artifacts/` 保存当前候选稿和临时检查文件。
- 所有可复用 Markdown 文档使用 UTF-8，避免乱码。

## 隐私和安全

- 公共 README、模板和 skill 文件中不要写入个人目录、用户名、私有课程路径、凭证或私有链接。
- 项目本地记录优先使用 `workflow_outputs/...` 这样的相对路径。
- 未经用户明确同意，不要把私人论文或课件上传到在线编辑器。

## License

MIT License. See `LICENSE`.
