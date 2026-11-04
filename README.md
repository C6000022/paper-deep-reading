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

## 首次配置：安装后还需要完成这一步

将 [个人配置模板](skills/paper-deep-reading/references/profile.example.md) 复制到当前操作系统用户主目录下的：

```text
~/.codex/paper-deep-reading.local.md
```

这里的 `~` 表示当前用户主目录；在 Windows 中，可以通过 PowerShell 的 `$env:USERPROFILE` 查看。技能安装目录和个人配置目录是两个不同位置。

编辑复制后的文件，将 `<ABSOLUTE_OUTPUT_ROOT>` 替换成自己的研究笔记库绝对路径，并确认期刊分流、文件名和同名追加规则。研究背景来源可以保持为空，空值只会限制“与本人研究的关系”这一节。

匿名模板默认将未匹配或无法识别期刊的笔记保存到输出根目录下的 `Others` 子文件夹。论文所在位置是输入路径，笔记输出根目录需由使用者另外指定。

该配置是由模型阅读的 Markdown，不需要安装配置解析器。模板中的输出路径占位符必须替换。配置缺失或必要值未填写时，技能会要求补充配置，不会自行猜测输出位置。详细字段见 [配置说明](skills/paper-deep-reading/references/configuration.md)。

个人配置保存在本仓库之外。分享本项目时，请仅分享匿名模板和通用指令，不要一并提交个人配置、研究库、论文 PDF 或笔记。

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
