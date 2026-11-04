# Paper Deep Reading · 论文精读

用于 Codex 等支持 Agent Skills 的环境：对学术 PDF 进行完整、批判性的精读，并将带有证据定位的 Markdown 笔记写入使用者配置的本地研究库。

An instruction-based Agent Skill for critical reading of scholarly PDFs, with evidence-traceable Markdown notes and a private, locally configured research vault.

## 能做什么

- 分析研究问题、材料与条件、方法、主要结果、机制解释和局限性。
- 为关键数据、参数和结论标注 PDF 文件页码及图表编号。
- 区分论文报告的事实、作者的解释和分析者的推断。
- 根据使用者提供的研究背景，讨论论文的适用范围和可借鉴之处。
- 每篇论文单独生成笔记；遇到同名笔记时，按个人配置追加指定章节并保留原文。

这是工作流指令与模板，不是独立的 PDF 解析程序。输出质量取决于模型、论文可读性和运行环境提供的工具。

## 运行条件与适用范围

运行环境需要支持读取技能文件、读取本地 PDF、提取文字、查看必要的页面或图表，以及写入本地 Markdown 文件。PDF 渲染、文字提取和文件访问由宿主环境提供；本仓库不附带模型、OCR 引擎或 PDF 处理程序。

本项目按 Codex 的本地文件工作流整理。其他支持 Agent Skills 的宿主也需要具备上述能力，并支持技能使用的个人配置路径；仅能处理聊天附件、不能写入本地研究库的环境不满足完整工作流。

扫描件或图表密集的论文可能需要宿主提供 OCR 或视觉阅读能力。核心内容无法可靠读取时，技能会停止该篇论文的笔记写入并说明原因。

## 安装

在 Codex 中，可以让内置安装器从仓库的技能子目录安装：

```text
使用 $skill-installer 从以下地址安装 paper-deep-reading：
https://github.com/C6000022/paper-deep-reading/tree/main/skills/paper-deep-reading
如果已有同名技能，请先说明现有位置，不要直接覆盖。
```

也可以下载本仓库，将 `skills/paper-deep-reading` 文件夹放入 Codex 的个人技能目录，例如 `~/.agents/skills/`。目录中必须保留 `SKILL.md`、`agents/` 和 `references/`。已有同名技能时，应先比较版本再决定如何更新。

如果安装后技能未出现，重启 Codex。安装方式和本地发现目录参见 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

## 第一次使用：提供论文，选择笔记保存位置

安装完成后，可以直接这样说。下面的路径仅为示例，请替换成自己的路径：

```text
用 $paper-deep-reading 精读 E:\Papers\paper.pdf。
```

如果没有现成的保存设置，Codex 会先询问你希望把笔记保存在哪里，并告知本机的具体默认位置：当前使用者“文档”目录下的 `PaperNotes\General`。文档目录由操作系统识别，不假定每台电脑都有 E 盘，也不把论文所在文件夹当作笔记目录。

这是可选的保存偏好询问。Codex 可以在等你回复时继续阅读论文；给你合理的回复机会后，如果到保存笔记时仍没有指定其他位置，就采用已告知的默认位置。若你明确给出另一处笔记总文件夹，例如 `E:\ReadingNotes`，默认分类笔记就保存到该文件夹下的 `General`。已经明确提供位置时，不重复询问。

确定位置后，Codex 按模板建立本机的个人配置，记住这次使用的设置；你无需手动复制或编辑配置文件。默认文件名采用“年份 - 论文正式题目.md”，默认使用简体中文，研究背景来源和期刊分类映射均可暂时留空。

下次直接提供另一份 PDF 即可沿用设置。需要更换保存位置时，可以说“以后把精读笔记保存到另一个完整路径”；Codex 应只更新对应设置，并保留其他个人偏好和既有笔记。

个人配置是一份记住保存位置和格式偏好的本地文本文件，保存在使用者的用户目录中，不会放进公开仓库。配置文件位置、字段说明和可选的手动配置方法见 [配置说明](skills/paper-deep-reading/references/configuration.md)。如果运行环境无法建立或读取配置，Codex 应说明原因，不得声称已经保存设置。

## 使用示例

提供论文 PDF 或本地文件路径后，在 Codex 中输入：

```text
用 $paper-deep-reading 精读这篇论文，按照我的本地配置生成完整笔记。
```

批量处理时：

```text
用 $paper-deep-reading 分别精读这些 PDF，每篇独立处理。
某篇无法读取时，说明原因并继续其他论文。
```

关键结果按 PDF 文件页码定位：文件的第一页计为 PDF 第 1 页，与论文印刷页码可能不同。笔记的通用结构见 [精读模板](skills/paper-deep-reading/references/note-template.md)。

## 证据边界

技能主要依据提供的论文，不通过网络补造缺失数据或机制。“创新性”部分评估论文声称的贡献及其证据，不能仅凭单篇论文证明领域首次；需要独立的文献新颖性核查时，应另行明确请求并提供或授权检索比较文献。

没有配置研究背景来源时，技能仍可完成论文分析，但会明确说明无法充分判断与使用者研究的关系。关键科学判断应回到 PDF 中核对。

## 仓库结构与插件清单

```text
paper-deep-reading/
├── README.md
├── LICENSE
├── plugin.json
├── .gitignore
└── skills/
    └── paper-deep-reading/
        ├── SKILL.md
        ├── LICENSE
        ├── agents/openai.yaml
        └── references/
            ├── configuration.md
            ├── profile.example.md
            └── note-template.md
```

根目录的 `plugin.json` 提供最小插件身份信息，便于后续按 [OpenAI 官方插件打包规范](https://developers.openai.com/plugins/build/plugins) 分发。GitHub 托管、作为独立技能安装，以及通过官方插件目录审核上架，是不同的交付步骤；仓库中提供清单并不表示已经通过目录审核。

## 贡献与许可

欢迎通过 GitHub Issues 或 Pull Requests 报告问题和改进工作流。提交问题时，请描述触发请求、宿主环境和预期行为，并使用匿名片段；不要上传私人研究数据或未经授权的论文全文。

Copyright (c) 2026 C6000022。项目文件采用 [MIT License](LICENSE)。论文、研究背景资料和使用者的笔记不随本项目发布，也不因使用本技能而获得本项目的许可。
