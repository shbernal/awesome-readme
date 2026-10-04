<a name="readme-top"></a>

# Navigation

A README is 1 long page. Navigation lets a newcomer jump to the part they came for, like install or quickstart, without scrolling past the rest.

## Where it goes

- 1 centered row right under the header, between 2 `---` rules.
- 3 to 6 entries. Pick the questions a newcomer asks, in the order they ask them.
- Entries can point to sections on the page (`#install`), to files (`docs/`, `CONTRIBUTING.md`) or to a docs site. Mixing is fine.
- A language switcher, if any, gets its own row, so it doesn't read as a section.

## Pick a style

| Style | Effort | Looks | Light and dark |
| :--- | :---: | :--- | :--- |
| Plain links | Low | Text | Follows the theme |
| `<kbd>` buttons | Low | Keyboard keys | Follows the theme |
| Badge buttons | Medium | Same as the badge row | Opaque, reads on both |
| Image buttons | High | Anything you draw | Needs 2 versions |

## Plain links

Links separated by a character.

<p align="center"><a href="#plain-links">Plain links</a> • <a href="#kbd-buttons">kbd buttons</a> • <a href="#badge-buttons">Badge buttons</a> • <a href="#image-buttons">Image buttons</a></p>

```markdown
[Install](#install) • [Quickstart](#quickstart) • [Usage](#usage) • [Docs](docs/)
```

| Separator | Character | Renders |
| :--- | :---: | :---: |
| Bullet | `•` (U+2022) | <a href="#plain-links">Plain links</a> • <a href="#kbd-buttons">kbd buttons</a> • <a href="#badge-buttons">Badge buttons</a> |
| Middle dot | `·` (U+00B7) | <a href="#plain-links">Plain links</a> · <a href="#kbd-buttons">kbd buttons</a> · <a href="#badge-buttons">Badge buttons</a> |
| Pipe | `\|` | <a href="#plain-links">Plain links</a> \| <a href="#kbd-buttons">kbd buttons</a> \| <a href="#badge-buttons">Badge buttons</a> |
| Brackets | `[` `]` | [<a href="#plain-links">Plain links</a>] [<a href="#kbd-buttons">kbd buttons</a>] [<a href="#badge-buttons">Badge buttons</a>] |

- Wider gaps: pad the separator with `&nbsp;`, like `&nbsp;&nbsp;•&nbsp;&nbsp;`.

<p align="center"><a href="#plain-links">Plain links</a>&nbsp;&nbsp;&nbsp;•&nbsp;&nbsp;&nbsp;<a href="#kbd-buttons">kbd buttons</a>&nbsp;&nbsp;&nbsp;•&nbsp;&nbsp;&nbsp;<a href="#badge-buttons">Badge buttons</a></p>

- More weight: wrap the row in `<b>`, or the whole line in bold.

<p align="center"><b><a href="#plain-links">Plain links</a> • <a href="#kbd-buttons">kbd buttons</a> • <a href="#badge-buttons">Badge buttons</a></b></p>

- Bigger text: wrap the row in `<h3>`. It also makes the row a heading for screen readers, so prefer `<b>` unless size matters.

<h3 align="center"><a href="#plain-links">Plain links</a> • <a href="#kbd-buttons">kbd buttons</a> • <a href="#badge-buttons">Badge buttons</a></h3>

- For HTML links, put 1 link per line in the source with the separator at the end. Adding or removing an entry then changes 1 line.

```html
<p align="center">
  <a href="#install">Install</a> •
  <a href="#quickstart">Quickstart</a> •
  <a href="#usage">Usage</a>
</p>
```

## `<kbd>` buttons

GitHub draws `<kbd>` as a small key with a border. It's the cheapest way to make links look like buttons.

<p align="center"><a href="#plain-links"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;Plain links&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a> <a href="#kbd-buttons"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;kbd buttons&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a> <a href="#badge-buttons"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;Badge buttons&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a> <a href="#image-buttons"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;Image buttons&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a></p>

```html
<a href="#install"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;Install&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a> <a href="#quickstart"><kbd>&nbsp;<br>&nbsp;&nbsp;&nbsp;Quickstart&nbsp;&nbsp;&nbsp;<br>&nbsp;</kbd></a>
```

- GitHub fixes the text at 11px. A heading around it doesn't make it bigger.
- The padding centers the label in a bigger key. `&nbsp;` lines above and below set the height, and `&nbsp;` on each side sets the width. Keep the bottom `&nbsp;`, or the last break collapses and the label sits low instead of centered.

## Badge buttons

A shields.io static badge with only a message works as a button. It matches a badge row in the header and can carry a [Simple Icons](https://simpleicons.org) logo.

<p align="center"><a href="#plain-links"><img alt="Plain links" src="https://img.shields.io/badge/Plain_links-7aa2f7?style=for-the-badge"></a> <a href="#kbd-buttons"><img alt="kbd buttons" src="https://img.shields.io/badge/kbd_buttons-7aa2f7?style=for-the-badge"></a> <a href="#badge-buttons"><img alt="Badge buttons" src="https://img.shields.io/badge/Badge_buttons-7aa2f7?style=for-the-badge"></a> <a href="#image-buttons"><img alt="Image buttons" src="https://img.shields.io/badge/Image_buttons-7aa2f7?style=for-the-badge"></a></p>

With a logo:

<p align="center"><a href="#plain-links"><img alt="Install" src="https://img.shields.io/badge/Install-7aa2f7?style=for-the-badge&logo=gnubash&logoColor=white"></a> <a href="#kbd-buttons"><img alt="Docs" src="https://img.shields.io/badge/Docs-7aa2f7?style=for-the-badge&logo=readthedocs&logoColor=white"></a> <a href="#badge-buttons"><img alt="Discussions" src="https://img.shields.io/badge/Discussions-7aa2f7?style=for-the-badge&logo=github&logoColor=white"></a></p>

```markdown
[![Install][install-btn]](#install) [![Quickstart][quickstart-btn]](#quickstart)

[install-btn]: https://img.shields.io/badge/Install-7aa2f7?style=for-the-badge
[quickstart-btn]: https://img.shields.io/badge/Quickstart-7aa2f7?style=for-the-badge
```

- Use the same style as the badge row, but 1 color for all buttons, so they read as a set and not as status.
- Keep them on their own row, away from the status badges.
- See [badges](badges.md) for URL syntax and colors.

## Image buttons

Draw each button as an SVG, then link it. Full control over shape, color and font.

<p align="center"><a href="../README.md#what-a-readme-is-for"><picture><source media="(prefers-color-scheme: dark)" srcset="../assets/nav/criteria-dark.svg"><img alt="Criteria" src="../assets/nav/criteria-light.svg"></picture></a> <a href="../README.md#best-practices"><picture><source media="(prefers-color-scheme: dark)" srcset="../assets/nav/best-practices-dark.svg"><img alt="Best practices" src="../assets/nav/best-practices-light.svg"></picture></a> <a href="../README.md#examples"><picture><source media="(prefers-color-scheme: dark)" srcset="../assets/nav/examples-dark.svg"><img alt="Examples" src="../assets/nav/examples-light.svg"></picture></a></p>

```html
<a href="#install"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/nav/install-dark.svg"><img alt="Install" src="assets/nav/install-light.svg"></picture></a>
```

- 1 light and 1 dark SVG per button, switched with `<picture>`. See [light and dark](light-and-dark.md).
- Convert the text to outlines. SVGs in `<img>` can't load fonts.
- Build the gap between buttons into each SVG as transparent margin. The space between 2 images is 1 character wide and can't be tuned.
- Give every button the same height, so the row lines up.
- Put the label in `alt`, so the row still reads where images are blocked.
- Keep each `<a>` on 1 line. A line break inside it adds an underlined space.

## Table of contents

GitHub generates an outline for every README, from the list icon at the top right of the file. For a short README, that's enough.

For a long one, add a list of section links after the intro:

- [Plain links](#plain-links)
- [`<kbd>` buttons](#kbd-buttons)
- [Table of contents](#table-of-contents)
  - [Back to top](#back-to-top)

```markdown
- [Install](#install)
- [Quickstart](#quickstart)
- [Configuration](#configuration)
  - [Themes](#themes)
```

- 1 level of nesting at most.
- Collapse it with `<details>`, so it doesn't push the content down:

<details>
<summary>Contents</summary>

- [Plain links](#plain-links)
- [`<kbd>` buttons](#kbd-buttons)
- [Badge buttons](#badge-buttons)
- [Image buttons](#image-buttons)

</details>

```html
<details>
<summary>Contents</summary>

- [Install](#install)
- [Quickstart](#quickstart)

</details>
```

- Leave a blank line after `<summary>` and before `</details>`, or GitHub won't render the markdown inside.

## Back to top

For a long README, a link at the end of each section returns to the header.

<div align="right"><a href="#readme-top">Back to top</a></div>

```markdown
<div align="right"><a href="#readme-top">Back to top</a></div>
```

- Put an anchor at the top of the file with `<a name="readme-top"></a>`. `#top` goes to the top of the GitHub page, not the README.
- Keep it small with `<sup>`, or make it a badge to match badge buttons.

<div align="right"><sup><a href="#readme-top">Back to top</a></sup></div>
<div align="right"><a href="#readme-top"><img alt="Back to top" src="https://img.shields.io/badge/Back_to_top-7aa2f7?style=for-the-badge"></a></div>

## Paths by reader

When readers come for different reasons, open with 1 line per reader:

- New here? Start with [where it goes](#where-it-goes) and [pick a style](#pick-a-style).
- Building buttons? See [image buttons](#image-buttons).
- Long README? Read [table of contents](#table-of-contents).

```markdown
- New here? Start with [what it is](#what-it-is) and [quickstart](#quickstart).
- Building from source? See [build](#build).
- Want to contribute? Read [CONTRIBUTING.md](CONTRIBUTING.md).
```

## Anchors

GitHub builds a section's anchor from its heading:

| Heading | Anchor |
| :--- | :--- |
| `## Install` | `#install` |
| `## How it works` | `#how-it-works` |
| `## Why?` | `#why` |
| `## ✨ Features` | `#-features` |
| A second `## Usage` | `#usage-1` |

- Lowercase, spaces become `-`, punctuation drops out. An emoji drops out too but leaves its space, hence the leading `-`.
- Renaming a heading breaks every link to it. Check the nav after any rename.
- For a stable anchor, add `<a name="install"></a>` above the heading.

## Inside a centered block

- GitHub strips `style`, `class` and `target`. Layout comes from tags and attributes like `align`, `width` and `height`, never CSS.
- Markdown inside `<div align="center">` only renders with a blank line after the opening tag and before the closing one.
