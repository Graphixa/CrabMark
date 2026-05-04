# CrabMark Specification (v0.1 Draft)

## 1. Overview

**CrabMark** is a Markdown superset designed to standardise commonly used extensions while maintaining compatibility with CommonMark and GitHub Flavoured Markdown (GFM).

CrabMark aims to:

* Preserve plain-text readability
* Minimise new syntax
* Consolidate widely adopted extensions
* Provide a consistent, extensible rendering model

---

## 2. Design Principles

### 2.1 Compatibility

* All valid [CommonMark](https://commonmark.org/) is valid CrabMark
* [GFM](https://github.github.com/gfm/) features are considered baseline where applicable

### 2.2 Minimal Syntax Expansion

* Prefer existing, widely used syntax (Pandoc, MultiMarkdown, GFM)
* Avoid introducing new syntactic forms unless necessary

### 2.3 Clear Separation

* **Inline features** → lightweight text semantics
* **Block features** → fenced rendering engines

### 2.4 Extensibility

* All advanced rendering is handled via fenced blocks

---

## 3. Inline Syntax

### 3.1 Superscript

```
^text^
```

### 3.2 Subscript

```
~text~
```

### 3.3 Strikethrough

```
~~text~~
```

### 3.4 Insertion

```
{++text++}
```

### 3.5 Deletion

```
{--text--}
```

### 3.6 Highlight

```
==text==
```

### 3.7 Footnotes

Reference:

```
Text[^1]
```

Definition:

```
[^1]: Footnote content
```

### 3.8 Inline Math

```
$E = mc^2$
```

---

## 4. Block Syntax

### 4.1 Fenced Block Model

All structured or renderable content uses fenced blocks:

````markdown
```<type>
<content>
```
````

Where `<type>` defines the rendering engine.

---

### 4.2 Display Math

````markdown
```math
E = mc^2
```
````

---

### 4.3 Mermaid Diagrams

````markdown
```mermaid
graph TD
  A --> B
```
````

---

### 4.4 Charts / Data Visualisation

````markdown
```chart
{ "type": "bar" }
```
````

---

### 4.5 Task Blocks (Optional Structured Form)

Inline tasks remain standard:

```
- [ ] Task
- [x] Done
```

Optional structured block:

````markdown
```tasks
- [ ] Task
- [x] Done
```
````

---

## 5. Lists and Tables

### 5.1 Task Lists

```
- [ ] Task
- [x] Done
```

### 5.2 Tables

Standard GFM pipe tables:

```
| Col A | Col B |
|------|------|
| 1    | 2    |
```

---

## 6. Additional Syntax

### 6.1 Abbreviations

```
*[HTML]: HyperText Markup Language
```

### 6.2 Definition Lists

```
Term

: Definition
```

### 6.3 Table of Contents

```
{{TOC}}
```

---

## 7. Metadata

YAML frontmatter is supported:

```yaml
---
title: Example Document
author: Author Name
---
```

---

## 8. Parsing Rules

### 8.1 Precedence

1. Fenced blocks are parsed first
2. Inline syntax is parsed after block structure
3. Inline math takes precedence over other inline markers within `$...$`

### 8.2 Tilde Handling

* `~~text~~` → strikethrough
* `~text~` → subscript

Rule:

* Double tilde (`~~`) has precedence over single tilde (`~`)

---

## 9. Rendering Model

### 9.1 Block Types

| Type      | Category | Description                  |
| --------- | -------- | ---------------------------- |
| `math`    | Active   | Render via LaTeX engine      |
| `mermaid` | Active   | Render diagram               |
| `chart`   | Active   | Render data visualisation    |
| `tasks`   | Active   | Render interactive checklist |
| others    | Passive  | Render as code block         |

### 9.2 Active vs Passive Blocks

* **Active blocks** require a rendering engine
* **Passive blocks** render as standard code blocks if unsupported

### 9.3 Fallback Behaviour

If a renderer does not support a block type:

* Display as a standard fenced code block
* Preserve content without modification

---

## 10. Security Considerations

* Renderers must sanitise HTML output
* External engines (e.g. Mermaid) should be sandboxed
* No arbitrary script execution is permitted

---

## 11. Extension Model (Future)

CrabMark may support extension declarations:

```yaml
---
crabmark: 0.1
extensions:
  - math
  - mermaid
  - chart
---
```

---

## 12. Goals (Non-Normative)

CrabMark aims to:

* Reduce fragmentation across Markdown flavours
* Provide a predictable authoring experience
* Enable tooling interoperability
* Support technical, academic, and documentation workflows

---

## 13. Non-Goals

CrabMark does not:

* Replace CommonMark
* Introduce complex programming logic
* Require specific rendering engines

---

## 14. Status

This is a draft specification (v0.1).
Subject to iteration and refinement.

---
