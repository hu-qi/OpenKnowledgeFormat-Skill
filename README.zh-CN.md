# Open Knowledge Format Skill

[English](README.md)

一个可复用的 Agent Skill，用于创建、校验、转换和维护 [Open Knowledge Format](https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf) 知识包。

OKF 使用带 YAML frontmatter 的 Markdown 文件、目录级索引、更新日志、引用和普通 Markdown 交叉链接来组织知识。本 Skill 可以帮助 AI 编程 Agent 和知识 Agent 将分散的项目上下文整理成可移植、可读、可由 Agent 消费的知识包。

## 状态

当前是 v0.1 初版 Skill，主要覆盖 OKF 知识包的创建、转换、校验和维护。

## 这个 Skill 能做什么

- 从项目文档、数据结构、API、指标、运行手册和 Wiki 内容创建 OKF 知识包。
- 将已有资料转换为“一个概念一个 Markdown 文件”的 OKF 概念文档。
- 校验目录是否符合 OKF v0.1。
- 生成带 YAML frontmatter 的概念文档。
- 生成用于渐进式导航的 `index.md`。
- 生成用于变更追踪的 `log.md`。
- 为 OKF 文档补充引用、交叉链接、示例、标签和结构字段。
- 为数据、软件、产品和企业知识系统设计 OKF 目录结构。

## 什么时候使用

当你需要把分散的项目上下文整理成 OKF 兼容的知识包，并提供给 Agent、开发者、数据团队或文档系统使用时，可以使用这个 Skill。

典型场景：

- 为一个软件项目创建 OKF 知识包。
- 将 API 文档、数据 schema、指标定义和运行手册转换为 OKF 概念文件。
- 校验某个目录是否符合 OKF v0.1。
- 为 OKF 知识包生成 `index.md` 和 `log.md`。
- 为 Coding Agent、Data Agent 或内部知识工具准备可读取的项目上下文。

## 安装 / 使用

使用 skills CLI 安装：

```bash
npx skills add hu-qi/OpenKnowledgeFormat-Skill
```

也可以手动复制 `SKILL.md` 到你的 Agent Skill 目录。

典型本地目录结构：

```text
.codex/skills/open-knowledge-format/SKILL.md
```

## 示例 Prompt

```text
Create an OKF bundle for this Vue + mock data dashboard project.
```

```text
Convert these API docs and data schema notes into OKF concept files.
```

```text
Validate this okf/ directory against OKF v0.1 and report errors and warnings.
```

```text
Generate index.md and log.md files for this OKF bundle.
```

## 仓库结构

```text
.
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── examples/
│   └── software-project-okf/
├── templates/
│   └── concept.md
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md
    │   └── request.md
    └── pull_request_template.md
```

## OKF 参考资料

- [Google Cloud Blog：How the Open Knowledge Format can improve data sharing](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing)
- [OKF README](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/README.md)
- [OKF SPEC](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)

## License

MIT
