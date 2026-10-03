# Light and dark

GitHub renders READMEs on a white or a near-black background, depending on the viewer's theme. Every image has to read on both.

## Ship 2 versions

Make a light and a dark version of logos, banners, diagrams and buttons, and switch with `<picture>`:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img alt="project-name" src="assets/banner-light.svg">
</picture>
```

- GitHub matches `prefers-color-scheme` against the viewer's GitHub theme.
- The `<img>` is the fallback for npm, crates.io and other sites that ignore `<source>`. Point it at the version that works on white.
- Put the `alt` on the `<img>`. It covers both versions.
- To make an image a link, wrap the whole `<picture>` in `<a>`.

## Avoid

- `#gh-dark-mode-only` and `#gh-light-mode-only` URL fragments. GitHub hides the wrong one, but every other site shows both images.
- A `prefers-color-scheme` media query inside the SVG. It follows the OS setting, not the GitHub theme, so it breaks for anyone whose 2 settings differ.
- Black or dark gray lines on a transparent background. They vanish in dark mode.

## Images with 1 version

- Screenshots and photos already have their own background. Leave them as they are.
- For a logo or diagram you can't make 2 versions of, give it a solid background and rounded corners, so it reads as a card on either theme.

## Diagrams

- Mermaid diagrams follow the GitHub theme on their own. Don't hardcode colors in them.
- For exported diagrams, export twice with a light and a dark theme, and switch with `<picture>`.

## SVG text

- GitHub shows SVGs through `<img>`, which can't load web fonts. Text falls back to whatever font the viewer has.
- Convert text to outlines before committing, for example with Inkscape's Path > Object to Path.

## Check

- Switch the GitHub theme in Settings > Appearance and look at the rendered README in both.
- Check the npm or crates.io page too, if the project publishes there.
