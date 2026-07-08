# Marp 论文汇报工作流

## 目标

把论文型 Marp/Markdown PPT 制作变成可追踪、可版本化、但不过度消耗时间和 token 的流程。默认选择能安全满足当前需求的最轻模式；只有用户要求或出现证据风险时才升级。

## 最小可行流程

处理任务前先选择一种模式，并简短说明：

- `quick_edit`：文字、样式、小布局修改，不需要论文证据。
- `fast_figure_fill`：用户已提供可用图表素材，或图表身份已经明确。
- `delivery_package`：用户明确要求打包某个版本或文件。
- `full_paper_audit`：用户要求论文下载、图表提取、事实核查、引用审计、广泛证据型改稿，或快速模式无法安全完成。

`quick_edit`、`fast_figure_fill`、`delivery_package` 只写 compact log。只有 `full_paper_audit` 才创建完整 paper manifest、论文摘要和 claim record。

## quick_edit

适用于只改文字、局部样式、少量页面布局的问题。

默认做：

- 定位用户指定页面或受影响片段。
- 只修改请求范围。
- 只检查变更页和必要相邻页。
- 记录 compact log：版本、页码、命令/输出、检查结论、未解决问题。

默认不做：

- 下载论文。
- 建证据库。
- 生成论文摘要。
- 建 claim record。
- 全 deck 检查。
- 导出 HTML/PPTX 或全页截图。

## fast_figure_fill

适用于用户已给图片、表格截图、裁剪图，或明确指定可直接使用的素材。

子路径：

- `provided_asset_insert`：素材就是目标图表或用户批准替代品，只做排版、说明、来源和局部视觉检查。
- `asset_identity_check`：素材身份不确定时，只做确认素材身份所需的最小证据检查。

默认做：

- 读取用户指定页或明确占位符。
- 摘录图表占位、用途、截图建议和教学点。
- 验证素材是否匹配请求的论文图号/表号，或是否为用户批准替代品。
- 插入素材，不改动图片像素，除非用户明确要求像素级标注。
- 写简短中文说明，开头使用 `Author et al. Fig. X:` 或 `Author et al. Table X:`。
- 添加或保留底部来源脚注。
- 只检查变更页和必要相邻页。
- 写 compact log。

默认不做：

- 下载论文。
- 从 PDF 重新抓图。
- 重建完整论文清单。
- 为所有论文生成中文摘要。
- 逐页事实核查。
- 运行与当前编辑无关的 workflow validation samples。

升级到 `full_paper_audit` 的条件：素材缺失或身份不清、图表号/文件名/占位要求冲突、解释需要图片之外的论文事实、引用元数据缺失且无法从已有记录推断，或用户明确要求下载论文、抓图、事实核查、完整审计。

## delivery_package

只在用户明确要求“打包某版本/文件”时使用。它是独立模式，不进入图表 Gate、事实核查、版本迭代或版式审查。

默认做：

- 确认用户指定的 Marp 源文件和同名/指定 PDF。
- 解析本地资源引用：Markdown 图片、HTML `src/href`、CSS `url(...)`，必要时包括 Marp/YAML 本地图片字段。
- 确认本地资源路径都是相对路径，并且能从 Marp 文件所在目录解析。
- 保留源码所需的相对目录关系生成 zip。
- 解压到临时目录复验相对路径。
- 验证后清理 staging/validation 临时目录，只保留最终 zip。

默认不做：

- 修改 Marp 内容。
- 重新导出 PDF，除非用户要求。
- 做图表占位 Gate。
- 建证据记录。
- 检查页面论述或排版。

## full_paper_audit

适用于用户要求下载/整理论文、从 PDF 提取图表、事实核查、生成论文摘要、审计引用、广泛修改论文依据内容，或快速模式无法安全完成。

完整模式要先列出待核查论文、缺失 PDF、引用缺口和需要核查的 claim，再按用户批准范围下载、总结和核查。

默认包含：

- 建立或更新 `workflow_outputs/papers/`、`figures/`、`artifacts/`、`versions/`。
- 创建版本化工作文件，不覆盖已批准版本。
- 建立 paper manifest。
- 为下载或用户提供的论文写 150-300 字中文摘要。
- 对用户批准范围内的 claim 做事实核查。
- 按图表占位 Gate 选择原图、裁剪图或简化图。
- 导出 PDF 并检查代表页、变更页和受共享 CSS/主题影响的页面。
- 写完整版本日志。

## 图表占位 Gate

填充或替换图表占位前，必须记录：

- 页码。
- 原始图表占位文本。
- 用途。
- 截图建议。
- 周围论证目标或教学点。
- 所选模式。

素材必须匹配请求的论文、图号/表号、用途和截图建议；偏离时必须有用户批准并写入日志。没有素材能满足要求时停止，不编造替代图。

## 版本与记录

- 不把源 deck 当作唯一副本编辑。
- 正式版本放 `workflow_outputs/versions/`，候选稿和临时检查放 `workflow_outputs/artifacts/`。
- 已批准版本不可覆盖；修正时创建下一版本并记录原因。
- 小任务写 compact log；完整审计写完整日志。
- 用户报告问题时，把问题和修复尝试写入日志，不静默替换历史。

## 导出与检查

- 小改和快速填图只检查变更页和必要相邻页。
- 不默认导出 HTML/PPTX 或全页截图。
- PDF 失败时先记录失败并判断是否与路径/素材无关；只有用户接受或项目已验证 fallback 时才走浏览器 fallback。
- standalone HTML 仅用于调试或用户要求，不作为默认交付物。

## workflow validation samples

只有在测试或改进 workflow/skill 本身时才运行 2-3 个代表页完整闭环。普通 quick edit、fast figure fill、delivery package 不运行 validation samples。

## 交付

- `quick_edit`：交付用户要求的新版本 Marp/PDF 或指定输出。
- `fast_figure_fill`：交付更新版本、PDF 预览和 compact log。
- `delivery_package`：交付 zip 和路径验证结果。
- `full_paper_audit`：额外交付 manifest、paper summaries、fact-check records 和完整版本日志。
