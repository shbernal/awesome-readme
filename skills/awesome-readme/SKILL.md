---
name: awesome-readme
description: use when writing a project's README.md
---

A README is for someone who just landed on the repo. Write for them, not for contributors or maintainers.

## Process

1. Read the project first. Find what it does, who it's for, the 1-command install, and what it competes with.
2. List the files that already exist (`docs/`, `CONTRIBUTING.md`, `LICENSE`, `CHANGELOG.md`). Anything they cover stays out of the README and gets a link at most.
3. Draft using the structure below.
4. Check every rule in "Never" against the draft.
5. Run the prose through the unslop skill if it's available.

## What goes in

In this order, skipping what the project doesn't have:

1. Header. Logo or banner, name, 1-line description, badges, section links.
2. Demo. A gif, video or screenshot, before the first paragraph.
3. What it is. 2 or 3 sentences, then the main features as short bullets.
4. Why. What problem it solves, or how it compares to similar projects. Use a table for comparisons.
5. Install. The shortest path to a working install.
6. Quickstart. A few numbered steps or a short tutorial that shows the first real use.
7. How it works. A short overview, with a diagram if the architecture isn't obvious.
8. More. Links to `docs/` and other guides.

## What stays out

| Content | Where it goes |
| --- | --- |
| Full documentation, feature specs, every command | `docs/` |
| Dev setup, build, test and lint commands, contribution rules | `CONTRIBUTING.md` |
| License text or a license section | `LICENSE` (GitHub already shows it) |
| Release notes, "what's new in v3" | `CHANGELOG.md` or GitHub releases |
| Guidance for AI agents | `AGENTS.md` |

## Header

- Center the header block with `<div align="center">`.
- Logo or banner on top. If the project has none, use the name as a heading and say so to the user.
- 1 line that says what the project does. Fewer words is better. "Find, verify, and analyze leaked credentials" is the bar.
- shields.io badges only for facts a newcomer cares about, like version, license, CI status, downloads. Match their style to each other.
- Section links as 1 centered row between 2 `---` rules. Pick by effort:
  - Low effort: plain links separated by bullets (`•`, U+2022) or pipes (`|`).
  - Easy, little customization: `<kbd>` buttons. GitHub fixes their text at 11px.
  - Full control: SVG buttons, 1 light and 1 dark SVG per button. Build the gap between buttons into each SVG as transparent margin, and convert the text to outlines, since SVGs in `<img>` can't load fonts.

```markdown
[Install](#install) • [Quickstart](#quickstart) • [Usage](#usage)
```

```markdown
<a href="#install"><kbd>Install</kbd></a> <a href="#quickstart"><kbd>Quickstart</kbd></a>
```

```markdown
<a href="#install"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/install-dark.svg"><img alt="Install" src="assets/nav/install-light.svg"></picture></a>
<a href="#quickstart"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/quickstart-dark.svg"><img alt="Quickstart" src="assets/nav/quickstart-light.svg"></picture></a>
```

## Visuals

- Show before telling. The demo goes above the first paragraph.
- Prefer a gif or video over a static screenshot for anything interactive. For terminal tools, a VHS or asciinema recording. For GUI and web apps, a screen recording converted with gifski.
- Put images next to the feature they show, not all in 1 gallery, unless the output itself is the selling point.
- Use 1 diagram that explains the project at a glance when there is one to draw. Use mermaid for architecture and data flow.
- Put a chart next to any benchmark table.
- Show logos of supported integrations instead of a bullet list of names.
- If you can't produce a visual, leave a commented placeholder and tell the user what to record. Never invent image URLs.

## Light and dark

- Every image has to read on GitHub's light and dark themes. Watch for dark lines on transparent backgrounds.
- Switch between light and dark versions with `<picture>`, with the light one as the `<img>` fallback. Not with `#gh-dark-mode-only` fragments.
- If an image has only 1 version and won't read on both themes, tell the user which one and what to fix.

## Install

- Only the package manager the project uses. Never list npm, yarn, pnpm and bun side by side.
- 1 code block per command, so the copy button grabs exactly that command.
- No comments inside install code blocks. Put the explanation in a sentence above.
- 1 command if possible. For several platforms, use 1-line bullets linking to details, or `<details>` blocks per platform.

## Text

- 1 idea per line. Break any paragraph over 3 sentences.
- Short, straight-to-the-point section titles in sentence case, like "Why?", "Install", "Usage".
- Tables for comparisons, compatibility and supported targets. Only columns a reader would use to decide.
- Describe what the project lets you do, not how it's built.
- For a library, describe capabilities at the API level. For a CLI, TUI or app, describe main uses and how to start.
- Show the main commands, not all of them. Link to the full reference.
- Add a "Lineage" section when the project evolved from prior projects, instead of calling it a fork.

## Never

- Walls of text.
- Em dashes, decorative emojis in headings or bullets, title case headings.
- Puffery like "blazing fast", "powerful", "seamless", "robust". Give the number or the mechanism.
- A License, Contributing, Changelog or Development section that repeats another file.
- Comments inside copyable code blocks.
- Every command or every option. That's `docs/`.
- Badges for vanity metrics, or more than 1 row of them.
- Images that only read on 1 theme.
