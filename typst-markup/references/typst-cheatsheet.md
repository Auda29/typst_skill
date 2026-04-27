# Typst Cheatsheet for Coding Agents

Use this reference when writing `.typ` files, converting Markdown to Typst, or reviewing generated Typst syntax.

Sources checked while creating this skill:

- Typst syntax reference: https://typst.app/docs/reference/syntax/
- Typst raw text/code reference: https://typst.app/docs/reference/text/raw/
- Typst link reference: https://typst.app/docs/reference/model/link/
- Typst table reference: https://typst.app/docs/reference/model/table/
- Typst compiler repository and CLI usage: https://github.com/typst/typst

## Core Model

Typst has three modes:

- Markup mode is the default for prose.
- Math mode is entered with `$...$`.
- Code mode is entered with `#`.

Common mode switches:

```typ
Number: #(1 + 2)
Inline math: $x^2$
#let name = [*Typst content*]
```

## Markdown to Typst Mapping

Prefer these mappings when replacing Markdown:

| Intent | Markdown habit | Typst |
| --- | --- | --- |
| Heading | `# Title` | `= Title` |
| Subheading | `## Section` | `== Section` |
| Strong | `**text**` | `*text*` |
| Emphasis | `*text*` or `_text_` | `_text_` |
| Inline code | `` `code` `` | `` `code` `` |
| Code block | fenced block | fenced raw block |
| Bullet list | `- item` | `- item` |
| Numbered list | `1. item` | `+ item` |
| Term list | often ad hoc | `/ Term: description` |
| Inline math | `$x$` | `$x$` |
| Display math | `$$...$$` | `$ ... $` with spaces |
| Link | `[text](url)` | `#link("url")[text]` |
| Image | `![alt](path)` | `#figure(image("path"), caption: [alt])` |
| Label | HTML anchors | `<label-name>` |
| Reference | Markdown link | `@label-name` |
| Table | pipe table | `#table(...)` |
| Comment | HTML comment | `// line` or `/* block */` |

## Document Skeleton

```typ
#set page(margin: 2.5cm)
#set text(size: 11pt)
#set heading(numbering: "1.")

= Document Title

Author or context line, if useful.

== Summary

Write normal prose in markup mode. Use _emphasis_, *strong emphasis*, and `raw text`.

== Details <details>

- First point
- Second point

See @details for the labeled section.
```

Keep preambles minimal. Add `#set document(title: "...")`, page size, fonts, headers, footers, numbering, or show rules only when requested or already used in the repo.

## Links, Labels, and References

```typ
#link("https://typst.app")[Typst]

= Architecture <architecture>

See @architecture.
```

Use kebab-case for labels and identifiers.

## Tables

Use `table` for semantic tabular data and `grid` only for visual layout.

```typ
#table(
  columns: (1fr, 2fr, auto),
  inset: 6pt,
  table.header([*Name*], [*Description*], [*Status*]),
  [Parser], [Converts source text into an AST], [Done],
  [Renderer], [Emits PDF output], [Planned],
)
```

For accessibility, use `table.header` for column headings. Wrap important tables in a `figure` with a useful caption when they need numbering or references.

## Figures and Images

```typ
#figure(
  image("images/architecture.png", width: 80%),
  caption: [System architecture],
) <fig-architecture>

See @fig-architecture.
```

Paths are strings. Relative paths resolve from the current Typst file; absolute paths start at the project root.

## Code Samples

Inline code:

```typ
Use `typst compile file.typ`.
```

Block code with highlighting:

````typ
```ts
export function render() {
  return "typst";
}
```
````

Typst supports language tags such as `typ`, `typc`, and `typm` for Typst markup, code, and math examples.

## Math

```typ
Inline equation: $E = m c^2$.

$ integral_0^1 x^2 dif x = 1/3 $
```

Inline math has no surrounding spaces inside `$...$`. Block math has spaces after the opening `$` and before the closing `$`.

## Functions, Set Rules, and Show Rules

Use code mode with `#` for expressions and definitions:

```typ
#let product = "Typst"
This document uses #product.
```

Use set rules for global defaults:

```typ
#set page(margin: 2.5cm)
#set heading(numbering: "1.")
```

Use show rules only when document styling requires them:

```typ
#show link: underline
```

## Conversion Pitfalls

- Do not preserve Markdown frontmatter unless another tool consumes it. Typst files normally start directly with Typst code or markup.
- Escape literal `#`, `$`, and other special characters with a backslash when Typst would otherwise parse them.
- Replace Markdown task lists with normal lists unless a custom checkbox macro exists.
- Replace HTML snippets with Typst functions or raw blocks. Do not assume arbitrary HTML is valid Typst.
- Convert Markdown pipe tables to `#table(...)`; pipe tables are not Typst table syntax.
- Check nested list indentation manually after conversion.

## Validation

Prefer the Typst CLI when available:

```powershell
typst compile file.typ
typst watch file.typ
typst compile --root .. file.typ
```

If validation fails, fix the first syntax error, rerun, and continue until compilation succeeds. If the CLI is unavailable, report that the output was reviewed but not compiled.
