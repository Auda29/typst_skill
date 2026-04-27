# Typst Markup Skill

`typst-markup` is a Codex/Coding Agent skill that makes Typst the preferred format for document-like artifacts. It helps agents write `.typ` files, convert Markdown-style documents to Typst, and avoid common Markdown habits that are invalid in Typst.

The skill is intentionally small: the main `SKILL.md` defines agent behavior, while the Typst syntax details live in a separate reference file that agents can load only when needed.

## What It Does

- Prefer `.typ` files over `.md` files for reports, specs, papers, handouts, and other document artifacts.
- Convert common Markdown constructs to idiomatic Typst.
- Provide defaults for headings, lists, links, code blocks, tables, figures, labels, references, and math.
- Encourage validation with `typst compile` when the Typst CLI is available.
- Keep the skill usable for Codex and adaptable for other coding agents that support skill-like instruction bundles.

## Repository Layout

```text
typst-markup/
  SKILL.md
  agents/
    openai.yaml
  references/
    typst-cheatsheet.md
```

## Installation for Codex

Clone this repository, then copy or symlink the `typst-markup` folder into your Codex skills directory.

PowerShell example:

```powershell
git clone https://github.com/Auda29/typst_skill.git
Copy-Item -Recurse .\typst_skill\typst-markup "$env:USERPROFILE\.codex\skills\typst-markup"
```

After installation, invoke it explicitly:

```text
Use $typst-markup to draft this report as a Typst document instead of Markdown.
```

Or rely on implicit triggering for requests involving Typst, `.typ` files, Markdown-to-Typst conversion, or document artifacts that should be authored in Typst.

## Installation for Other Coding Agents

For agents without native Codex skill support, use the content of `typst-markup/SKILL.md` as the system or project instruction, and keep `typst-markup/references/typst-cheatsheet.md` available as an auxiliary reference.

Recommended behavior:

- Load `SKILL.md` for any task involving Typst or document artifacts.
- Load `references/typst-cheatsheet.md` only when syntax examples or conversion mappings are needed.
- Prefer writing final document artifacts to `.typ` files.

## Requirements

The skill itself has no runtime dependencies. To validate generated Typst documents locally, install the Typst CLI:

```powershell
winget install --id Typst.Typst
typst compile file.typ
```

## License

Apache-2.0. See [LICENSE](LICENSE).
