# Pi Typst Skill

`pi-typst-skill` is a [pi coding agent](https://pi.dev/) package that adds a `typst-markup` skill. It nudges pi to create document artifacts as Typst (`.typ`) instead of Markdown, and gives the agent compact syntax guidance for writing or converting Typst documents.

This is a skills-only package: it does not run extension code and has no runtime dependencies. The package is structured for `pi install`, npm publishing, and the [pi.dev package gallery](https://pi.dev/packages).

## Install

Install from GitHub:

```sh
pi install git:github.com/Auda29/typst_skill
```

Try it for a single session without installing permanently:

```sh
pi -e git:github.com/Auda29/typst_skill
```

If published to npm, install it like any other pi package:

```sh
pi install npm:pi-typst-skill
```

## Use

Ask pi for Typst output explicitly:

```text
Use $typst-markup to draft this technical report as a Typst document.
```

Typical prompts:

```text
Create a Typst project brief for this repository.
```

```text
Convert README.md into a clean .typ handout.
```

```text
Write the architecture notes as Typst instead of Markdown.
```

The skill tells pi to prefer `.typ` files for reports, specs, papers, handouts, and similar document artifacts, while still respecting existing project conventions.

## Package Layout

```text
package.json
typst-markup/
  SKILL.md
  references/
    typst-cheatsheet.md
  agents/
    openai.yaml
```

`package.json` declares the pi package:

```json
{
  "keywords": ["pi-package", "pi-skill"],
  "pi": {
    "skills": ["./typst-markup"]
  }
}
```

`typst-markup/SKILL.md` is the loaded skill instruction. `references/typst-cheatsheet.md` is loaded only when the agent needs syntax mappings or examples.

## What the Skill Covers

- Typst as the default format for document artifacts.
- Markdown-to-Typst conversion patterns.
- Typst headings, lists, links, labels, references, tables, figures, code blocks, and math.
- Validation with `typst compile` when the Typst CLI is installed.
- Fallback behavior when the CLI is unavailable.

## Typst CLI

The skill works without local dependencies, but generated documents should be compiled when possible:

```sh
typst compile file.typ
```

On Windows:

```powershell
winget install --id Typst.Typst
```

## Codex Compatibility

The `typst-markup` folder also follows the `SKILL.md` convention used by Codex-style skills. For Codex, copy or symlink that folder into the Codex skills directory.

## License

Apache-2.0. See [LICENSE](LICENSE).
