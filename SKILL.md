---
name: "open-knowledge-format"
description: "Use when creating, inspecting, validating, converting, or maintaining Open Knowledge Format (OKF) knowledge bundles made of Markdown files with YAML frontmatter, index files, logs, citations, and cross-links for human and AI-agent consumption."
---

# Open Knowledge Format Skill

## Purpose

Use this skill to create, inspect, validate, convert, and maintain knowledge bases that follow the Open Knowledge Format, abbreviated as OKF.

OKF is an open, vendor-neutral format for representing knowledge as a directory of Markdown files with YAML frontmatter. It is intended to be readable by humans, parseable by AI agents, portable across tools, and manageable in version control.

Use this skill when the user wants to:

- Build an OKF bundle from existing documents, schemas, APIs, metrics, runbooks, wiki pages, or project notes.
- Convert project knowledge into an agent-readable knowledge bundle or LLM wiki.
- Validate whether a directory follows OKF v0.1.
- Generate OKF concept documents.
- Generate or update `index.md` files for progressive disclosure.
- Generate or update `log.md` files for change history.
- Add citations, cross-links, schemas, examples, and tags to OKF documents.
- Design a knowledge catalog that can be consumed by coding agents, data agents, search tools, graph viewers, or static documentation sites.

## Core Concepts

### Knowledge Bundle

A Knowledge Bundle is a self-contained directory tree of Markdown files.

The bundle is the unit of exchange. It can live in:

- A Git repository.
- A subdirectory inside a larger repository.
- A zip or tarball.
- Any filesystem or static file host.

### Concept

A Concept is one unit of knowledge represented by one Markdown file.

A concept can describe:

- A database table.
- A dataset.
- A metric.
- An API endpoint.
- A business rule.
- A playbook.
- A runbook.
- A domain concept.
- A system component.
- A reference document.

The concept ID is the file path inside the bundle without the `.md` suffix.

Example file path:

```text
tables/orders.md
```

Concept ID:

```text
tables/orders
```

### Frontmatter

Every concept document must start with YAML frontmatter.

The only required field is:

```yaml
type:
```

Recommended fields are:

```yaml
title:
description:
resource:
tags:
timestamp:
```

Additional producer-defined fields are allowed and should be preserved.

### Body

The body is normal Markdown.

Prefer structured Markdown:

- Headings.
- Tables.
- Lists.
- Fenced code blocks.
- Examples.
- Citations.
- Cross-links.

There are no required body sections, but the following headings are conventional:

```markdown
# Schema
# Examples
# Citations
```

### Cross-links

Concepts should link to related concepts using standard Markdown links.

Preferred bundle-root link:

```markdown
See [customers](/tables/customers.md).
```

Relative links are also allowed:

```markdown
See [neighbor](./other.md).
```

A link from one concept to another expresses a relationship. The relationship type is described by the surrounding prose, not by a special link syntax.

Consumers must tolerate broken links.

### Reserved Files

The following filenames have special meaning and must not be used as normal concept documents:

```text
index.md
log.md
```

### index.md

An `index.md` file may appear in any directory.

It supports progressive disclosure, allowing humans and agents to see what is available before opening individual documents.

It usually contains grouped links:

```markdown
# Tables

* [Orders](orders.md) - One row per completed customer order.
* [Customers](customers.md) - One row per customer.

# Metrics

* [Weekly Active Users](../metrics/weekly_active_users.md) - Definition of WAU.
```

Normally, `index.md` should not contain frontmatter.

Exception: the bundle-root `index.md` may include frontmatter only when declaring the OKF version:

```yaml
---
okf_version: "0.1"
---
```

### log.md

A `log.md` file may appear at any level of the hierarchy.

It records chronological changes, newest first.

Date headings must use ISO date format:

```markdown
# Directory Update Log

## 2026-06-16

* **Creation**: Added [Orders](/tables/orders.md).
* **Update**: Added schema details to [Customers](/tables/customers.md).

## 2026-06-10

* **Initialization**: Created initial bundle structure.
```

### Citations

If the concept body makes claims based on external sources, add a `# Citations` section at the bottom.

Example:

```markdown
# Citations

[1] [BigQuery table schema](https://console.cloud.google.com/bigquery?p=acme&d=sales&t=orders)
[2] [Internal data quality runbook](https://wiki.example.com/data-quality)
```

Citation links may be:

- Absolute URLs.
- Bundle-relative paths.
- Paths into a `references/` directory.

## OKF v0.1 Conformance Rules

A bundle conforms to OKF v0.1 when:

1. Every non-reserved `.md` file contains parseable YAML frontmatter.
2. Every concept frontmatter contains a non-empty `type` field.
3. Reserved filenames follow their expected structure:
   - `index.md` is a directory listing.
   - `log.md` is an update history.

Consumers should be permissive.

Do not reject a bundle because of:

- Missing optional frontmatter fields.
- Unknown `type` values.
- Unknown extra frontmatter keys.
- Broken cross-links.
- Missing `index.md` files.

## Recommended Bundle Structure

For data systems:

```text
okf/
├── index.md
├── log.md
├── datasets/
│   ├── index.md
│   └── sales.md
├── tables/
│   ├── index.md
│   ├── orders.md
│   └── customers.md
├── metrics/
│   ├── index.md
│   └── weekly_active_users.md
├── playbooks/
│   ├── index.md
│   └── data_freshness_alert.md
└── references/
    ├── index.md
    └── bigquery_export_docs.md
```

For software engineering projects:

```text
okf/
├── index.md
├── log.md
├── systems/
│   ├── index.md
│   └── frontend_app.md
├── modules/
│   ├── index.md
│   └── auth_module.md
├── apis/
│   ├── index.md
│   └── login_api.md
├── concepts/
│   ├── index.md
│   └── user_session.md
├── runbooks/
│   ├── index.md
│   └── deploy_frontend.md
└── decisions/
    ├── index.md
    └── use_vue_stack.md
```

## Concept Document Template

Use this template when creating a new concept:

````markdown
---
type: <Concept Type>
title: <Human-readable title>
description: <One-sentence summary>
resource: <Optional URI for the underlying asset>
tags: [<tag1>, <tag2>]
timestamp: <ISO 8601 datetime>
---

# Overview

Describe what this concept is and why it matters.

# Details

Add structured details, definitions, constraints, ownership, lifecycle, or usage notes.

# Schema

Use this section when the concept has fields, columns, parameters, or structured attributes.

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique identifier. |

# Examples

```text
Add examples, queries, payloads, workflows, or commands.
```

# Relationships

Describe related concepts using Markdown links.

Example:

- Depends on [Example Concept](/path/to/example.md).
- Used by [Another Concept](/path/to/another.md).

# Citations

[1] [Source title](https://example.com)
````

## Type Suggestions

OKF does not define a central type registry. Use descriptive type names.

Recommended examples:

```text
BigQuery Dataset
BigQuery Table
Database Table
Metric
API Endpoint
API Schema
Business Concept
Playbook
Runbook
Reference
Decision
System
Module
Component
Data Pipeline
Event
Glossary Term
Policy
SOP
```

When consuming an OKF bundle, tolerate unknown types and treat them as generic concepts.

## Workflow: Create an OKF Bundle

When asked to create a bundle:

1. Identify the knowledge domain.
2. Propose a directory structure.
3. Extract candidate concepts.
4. Create one Markdown file per concept.
5. Add YAML frontmatter to every concept.
6. Add structured Markdown body sections.
7. Add cross-links between related concepts.
8. Add citations when claims come from sources.
9. Generate `index.md` files for directories.
10. Generate or update `log.md`.
11. Validate conformance.

## Workflow: Convert Existing Material to OKF

When converting existing docs, specs, code, APIs, schemas, or wiki pages:

1. Inventory all source materials.
2. Classify source materials into concepts.
3. Decide the target directory structure.
4. Split large documents into atomic concept files.
5. Preserve source references in `# Citations`.
6. Add `tags` and `description` fields for search and previews.
7. Add links between concepts.
8. Generate directory-level indexes.
9. Add an update log.
10. Report what was converted, what was skipped, and what needs manual review.

## Workflow: Validate an OKF Bundle

Check:

1. All `.md` files are UTF-8 Markdown.
2. `index.md` and `log.md` are handled as reserved files.
3. Every concept document starts with parseable YAML frontmatter.
4. Every concept frontmatter has a non-empty `type`.
5. Recommended fields are present where useful:
   - `title`
   - `description`
   - `resource`
   - `tags`
   - `timestamp`
6. Markdown links are syntactically valid.
7. Broken links are reported as warnings, not fatal errors.
8. `index.md` files list nearby concepts.
9. `log.md` date headings use `YYYY-MM-DD`.
10. Claims from external sources have citations.

Report validation results as:

```markdown
# OKF Validation Report

## Summary

- Bundle path:
- Concept files:
- Index files:
- Log files:
- Conformance:
- Errors:
- Warnings:

## Errors

## Warnings

## Recommendations
```

## Workflow: Generate index.md

For each directory:

1. Read all direct child concept files.
2. Extract `title` and `description` from frontmatter.
3. Group entries by subdirectory or type.
4. Generate relative links.
5. Keep the index concise.

Example:

```markdown
# Tables

* [Orders](orders.md) - One row per completed customer order.
* [Customers](customers.md) - One row per customer.

# Subdirectories

* [Metrics](../metrics/) - Business metrics and definitions.
```

## Workflow: Generate log.md

When adding or changing concepts:

1. Add the newest date heading first.
2. Use ISO date format.
3. Use short entries.
4. Link to affected concepts.

Example:

```markdown
# Directory Update Log

## 2026-06-16

* **Creation**: Added [Orders](/tables/orders.md).
* **Update**: Added join notes to [Customers](/tables/customers.md).
```

## Output Standards

When producing OKF content:

- Prefer clear Markdown.
- Keep one concept per file.
- Do not overfit to one cloud, database, model, or framework.
- Do not invent a strict type taxonomy.
- Do not reject unknown fields.
- Do not replace domain-specific schemas such as OpenAPI, Protobuf, Avro, or SQL DDL; reference them instead.
- Use absolute bundle-relative links when possible.
- Use citations when source material supports factual claims.
- Keep bundles useful for both humans and agents.

## Common Tasks

### Create a concept document

Input:

```text
Create an OKF concept for the Orders table.
```

Output:

```markdown
---
type: Database Table
title: Orders
description: One row per completed customer order.
resource: <table URI>
tags: [orders, sales, revenue]
timestamp: 2026-06-16T00:00:00Z
---

# Schema

| Column | Type | Description |
|---|---|---|
| `order_id` | string | Unique order identifier. |

# Relationships

Joined with [Customers](/tables/customers.md) on `customer_id`.

# Citations

[1] [Source title](https://example.com)
```

### Review an OKF bundle

Return:

```markdown
# OKF Review

## What works

## Conformance issues

## Structural issues

## Missing metadata

## Broken or weak links

## Suggested changes

## Next actions
```

### Design an OKF bundle for a project

Return:

```markdown
# Proposed OKF Bundle Structure

## Directory Tree

## Concept Types

## Initial Concept List

## Index Strategy

## Citation Strategy

## Maintenance Workflow
```

## Best Practices

- Treat OKF as knowledge as code.
- Store the bundle in Git.
- Review changes through pull requests.
- Use `index.md` for navigation.
- Use `log.md` for traceability.
- Use tags for cross-cutting categories.
- Keep concept files small enough for agents to load selectively.
- Prefer links over duplicated explanations.
- Put authoritative source links in `# Citations`.
- Let agents enrich the bundle, but keep humans in the review loop.

## Anti-patterns

Avoid:

- One huge Markdown file for everything.
- Missing `type` fields.
- Treating OKF as a rigid database schema.
- Inventing a mandatory global type registry.
- Embedding all source data instead of linking to domain-specific artifacts.
- Using screenshots as knowledge when structured text is available.
- Hiding knowledge behind proprietary APIs only.
- Creating directories without `index.md` when the bundle is meant for agent navigation.
- Omitting citations for factual claims from external sources.

## When to Ask for Clarification

Ask the user only when necessary:

- The target domain is unclear.
- The source material is missing.
- The user wants a specific directory convention.
- There is uncertainty about whether to create a full bundle or only a single concept.
- The output location or packaging format matters.

Otherwise, make a reasonable structure and proceed.
