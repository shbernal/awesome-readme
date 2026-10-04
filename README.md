<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img alt="awesome-readme" src="assets/banner-light.svg" width="100%">
</picture>

### Opinionated guide to READMEs for AI-driven development

[![Agent skill][skill-badge]][Skill]
[![Last commit][commit-badge]][commits]
[![License][license-badge]][license]

---

<a href="#what-a-readme-is-for"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/criteria-dark.svg"><img alt="Criteria" src="assets/nav/criteria-light.svg"></picture></a>
<a href="#best-practices"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/best-practices-dark.svg"><img alt="Best practices" src="assets/nav/best-practices-light.svg"></picture></a>
<a href="#examples"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/examples-dark.svg"><img alt="Examples" src="assets/nav/examples-light.svg"></picture></a>
<a href="#skill"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/skill-dark.svg"><img alt="Skill" src="assets/nav/skill-light.svg"></picture></a>
<a href="CONTRIBUTING.md"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/contribute-dark.svg"><img alt="Contribute" src="assets/nav/contribute-light.svg"></picture></a>

---

</div>

## Why this project?

While building projects with coding agents, I kept rewriting their READMEs. Over time, I have recognized some patterns and formed opinions on what makes a good README.

This repo is for people looking for inspiration, and for agents that need to be told what good looks like. The goal is to raise the bar for READMEs in AI-driven development.

The [skill](#skill) distills it all into key guidance. Your agent writes an elegant README with no effort on your part, so you can focus on what matters, like architecture and features.

## What a README is for

A README is for someone who just landed on the repo. They want to know what the project does, what using it looks like, and how to install it. That's it.

It should show:

- what it looks like
- the main features
- a quickstart guide
- a basic overview of how it works
- how it compares to similar projects

It should not repeat what other files already say.

| Content | Where it goes |
| --- | --- |
| Full documentation, feature specs | `docs/` |
| Dev setup, contribution rules | `CONTRIBUTING.md` |
| License terms | `LICENSE` |
| Release history | `CHANGELOG.md` or GitHub releases |
| Guidance for AI agents | `AGENTS.md` |

## Best practices

### Structure

- Order the sections the way a newcomer asks questions: header, demo, what it is, why, install, quickstart, how it works, further docs.
- Explain why the project exists before the install section.
- Skip the sections the project has nothing for.

### Header

- Logo or banner on top, project name in it.
- Centered header block with [shields.io](https://shields.io) badges in `for-the-badge` style, colored to match the project. [Gallery and recipes](docs/badges.md).
- A short description. Target 1 line.
- Section links under the header, styled with a bit of HTML. [Options](docs/navigation.md).

### Show, then tell

- Put the visuals before the first paragraph. A gif or video beats a static screenshot.
- Record real behavior, like a TUI or CLI output, with VHS or asciinema. [Recordings](docs/recordings.md).
- For a scene you can't record, like an agent session or an MCP call, generate an animated SVG. [How it's built](docs/animated-svg.md).
- Spread visuals through the README, next to the feature they show.
- Pick a diagram that explains the project at a glance.
- Show logos for supported integrations instead of a bullet list of names.
- A gallery for projects where the output is the selling point.
- Every image has to read on GitHub's light and dark themes. [Here's how](docs/light-and-dark.md).

### Text

- 1 idea per line. No walls of text.
- Short, straight-to-the-point section titles, like "Why?" or "Install".
- Tables for comparisons, compatibility and supported targets. Keep columns to what matters.
- Put a chart next to benchmark tables, and a mermaid diagram next to architecture explanations.
- A "Lineage" section for a project evolving from prior projects.

### Install and quickstart

- 1 code block per command, so GitHub's copy button grabs exactly that command. No comments inside the block.
- Install in 1 command when possible.
- List install options as 1-line bullets that link to the details, or put them in collapsible `<details>` sections.
- A step-by-step quickstart or short tutorial to show it's easy to use.

### Depth

- Show the main commands, not all of them. Link to the full reference.
- End with links to further docs for people who want more.
- A roadmap, if any, as a visual with clear phases.

## Examples

13 READMEs worth stealing from, grouped by kind of project.

### Developer CLIs

| Project | Takeaways |
| :---: | :--- |
| <a href="https://github.com/jdx/mise#readme"><img src="https://raw.githubusercontent.com/jdx/mise/main/docs/public/favicon.svg" height="32" alt="mise"><br>mise</a> | <ul><li>Centered header</li><li>Custom styled shields</li><li>Usage videos</li></ul> |
| <a href="https://github.com/evilmartians/lefthook#readme"><img src="https://raw.githubusercontent.com/evilmartians/lefthook/master/logo_sign.svg" height="32" alt="lefthook"><br>lefthook</a> | <ul><li>Short, to-the-point text that's easy to scan</li><li>Clear structure with why, usage with a TL;DR, and install with copyable commands</li></ul> |
| <a href="https://github.com/charmbracelet/gum#readme"><img src="https://stuff.charm.sh/gum/gum.png" height="32" alt="gum"><br>gum</a> | <ul><li>Logo and demo before any paragraph</li><li>Opens with a tutorial</li><li>Gifs spread across the README</li></ul> |
| <a href="https://github.com/ajeetdsouza/zoxide#readme"><img src="https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/contrib/logo-light.svg" height="32" alt="zoxide"><br>zoxide</a> | <ul><li>Collapsible sections per install method</li><li>Stylized demo gif</li></ul> |
| <a href="https://github.com/trufflesecurity/trufflehog#readme"><img src="https://storage.googleapis.com/trufflehog-static-sources/pixel_pig.png" height="32" alt="trufflehog"><br>trufflehog</a> | <ul><li>Icon and a 3-word description</li><li>Logos for what it scans</li><li>Stylized demo gif, 1-command install</li><li>Step-by-step quickstart</li></ul> |
| <a href="https://github.com/spicetify/cli#readme"><img src="https://github.com/spicetify.png" height="32" alt="spicetify"><br>spicetify</a> | <ul><li>Logo banner and shields</li><li>1-line description focused on the core</li><li>Features shown with images, original and modified side by side</li><li>Links out to install and user guides</li></ul> |

### Terminal and desktop

| Project | Takeaways |
| :---: | :--- |
| <a href="https://github.com/zellij-org/zellij#readme"><img src="https://raw.githubusercontent.com/zellij-org/zellij/main/assets/logo.png" height="32" alt="zellij"><br>zellij</a> | <ul><li>Logo, then a gif of it in use right away</li><li>Roadmap as a chart with 3 clear phases</li><li>1-word or question section titles</li></ul> |
| <a href="https://github.com/hyprwm/hyprland#readme"><img src="https://github.com/hyprwm.png" height="32" alt="Hyprland"><br>Hyprland</a> | <ul><li>Section links on top styled with HTML</li><li>Short feature list</li><li>Gallery of what people built with it</li></ul> |

### Markup and typesetting

| Project | Takeaways |
| :---: | :--- |
| <a href="https://github.com/typst/typst#readme"><img src="https://github.com/typst.png" height="32" alt="Typst"><br>typst</a> | <ul><li>Banner with the project name</li><li>Centered shields</li><li>Explanation and main features right after, as bullets</li><li>Side-by-side Typst source and rendered output</li></ul> |

### AI and agent tools

| Project | Takeaways |
| :---: | :--- |
| <a href="https://github.com/OpenHands/OpenHands#readme"><img src="https://raw.githubusercontent.com/OpenHands/OpenHands/main/public/favicon.svg" height="32" alt="OpenHands"><br>OpenHands</a> | <ul><li>Logo and shields on top</li><li>Quickstart guide</li><li>Architecture section with diagrams</li><li>Links to further docs at the end</li></ul> |
| <a href="https://github.com/nexu-io/open-design#readme"><img src="https://raw.githubusercontent.com/nexu-io/open-design/main/apps/web/public/app-icon.svg" height="32" alt="Open Design"><br>open-design</a> | <ul><li>Strong banner, centered sections below</li><li>Lots of images showing how to use it</li><li>Tight tables for competitor comparison and supported agents</li><li>"Lineage" section at the bottom instead of calling it a fork</li></ul> |

### Generators and assets

| Project | Takeaways |
| :---: | :--- |
| <a href="https://github.com/lowlighter/metrics#readme"><img src="https://raw.githubusercontent.com/lowlighter/metrics/master/source/app/web/statics/favicon.png" height="32" alt="metrics"><br>metrics</a> | <ul><li>Very visual, lots of output images</li><li>Setup options listed with links to detailed steps in another file</li></ul> |
| <a href="https://github.com/ryanoasis/nerd-fonts#readme"><img src="https://raw.githubusercontent.com/ryanoasis/nerd-fonts/master/images/nerd-fonts-character-logo-md.png" height="32" alt="Nerd Fonts"><br>nerd-fonts</a> | <ul><li>1 diagram that shows where each glyph set comes from</li><li>Download options as 1-sentence bullets with links</li><li>Font list as a table</li><li>font-patcher gets its own logo, marking it as a separate project inside the repo</li></ul> |

## Skill

[`skills/awesome-readme`](skills/awesome-readme/SKILL.md) turns all of the above into instructions for coding agents. Without them, agents tend to:

- write walls of text
- write slop, meaning puffery, em dashes, decorative emojis and title case headings
- add sections that belong in other files, like license, contributing, changelog and dev setup
- list install commands for every package manager instead of the one the project uses
- put comments inside install code blocks
- describe how the project is built instead of what it lets you do

Install it with [skills](https://github.com/vercel-labs/skills).

```sh
npx skills add shbernal/awesome-readme
```

For prose, pair it with the [unslop skill](https://github.com/cursor/plugins/blob/main/pstack/skills/unslop/SKILL.md).

<!----------------------------------------------------------------------------->

[Skill]: #skill
[commits]: https://github.com/shbernal/awesome-readme/commits/main
[license]: LICENSE

[skill-badge]: https://img.shields.io/badge/agent_skill-awesome--readme-9854f1?style=for-the-badge
[commit-badge]: https://img.shields.io/github/last-commit/shbernal/awesome-readme?style=for-the-badge&color=7aa2f7
[license-badge]: https://img.shields.io/github/license/shbernal/awesome-readme?style=for-the-badge&color=e0af68
