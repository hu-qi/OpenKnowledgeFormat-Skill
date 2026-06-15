# Open Knowledge Format Skill

A reusable Agent Skill for creating, validating, converting, and maintaining [Open Knowledge Format](https://github.com/GoogleCloudPlatform/knowledge-catalog/tree/main/okf) knowledge bundles.

OKF represents knowledge as Markdown files with YAML frontmatter, directory-level indexes, update logs, citations, and normal Markdown cross-links. This skill helps AI coding agents and knowledge agents turn scattered project context into portable, human-readable, agent-readable knowledge bundles.

## Keywords

`open-knowledge-format`, `okf`, `knowledge-catalog`, `knowledge-bundle`, `llm-wiki`, `agent-skill`, `codex-skill`, `ai-agent`, `knowledge-as-code`, `markdown`, `yaml-frontmatter`, `metadata`, `data-catalog`, `semantic-layer`, `context-engineering`, `agent-context`, `knowledge-graph`, `data-governance`, `documentation`, `github`, `open-standard`

## What this skill does

- Creates OKF bundles from project docs, schemas, APIs, metrics, runbooks, and wiki content.
- Converts existing material into one-concept-per-file Markdown documents.
- Validates OKF v0.1 conformance.
- Generates concept documents with YAML frontmatter.
- Generates `index.md` files for progressive disclosure.
- Generates `log.md` files for traceable knowledge changes.
- Adds citations, cross-links, examples, tags, and schema sections.
- Designs OKF bundle structures for data, software, product, and enterprise knowledge systems.

## Install / Use

Use this repository as a skill source, or copy `SKILL.md` into your agent's skill directory.

Typical local layout:

```text
.codex/skills/open-knowledge-format/SKILL.md
```

Or, when used as a standalone skill repository:

```text
OpenKnowledgeFormat-Skill/
├── SKILL.md
├── README.md
├── examples/
└── templates/
```

## Example prompts

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

## Repository structure

```text
.
├── SKILL.md
├── README.md
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
    └── pull_request_template.md
```

## OKF references

- [Google Cloud blog: How the Open Knowledge Format can improve data sharing](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing)
- [OKF README](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/README.md)
- [OKF SPEC](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md)

## License

MIT
