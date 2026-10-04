# Recordings

A recording captures the real program running. Use one when the demo has to show real behavior: a TUI dashboard, a CLI's actual output, a GUI or web app.

If the scene can't be recorded, like an agent session or an MCP call, or you want full control over timing and layout, build an [animated SVG](animated-svg.md) instead.

## Pick a tool

| Project | Tool | Output |
|---|---|---|
| CLI or TUI, scripted | [VHS](https://github.com/charmbracelet/vhs) | GIF, MP4, WebM |
| CLI or TUI, typed live | [asciinema](https://asciinema.org) + [agg](https://github.com/asciinema/agg) | GIF |
| CLI, as a vector image | asciinema + [termsvg](https://github.com/MrMarble/termsvg) | Animated SVG |
| GUI or web app | Any screen recorder + [gifski](https://gif.ski) | GIF |
| Long walkthrough | Any screen recorder | MP4 uploaded to GitHub |
| Single frame of a terminal | [freeze](https://github.com/charmbracelet/freeze), [termshot](https://github.com/homeport/termshot) | PNG, SVG |

Skip svg-term-cli and termtosvg. The first hasn't changed since 2024 and the second is archived.

## VHS

VHS runs a `.tape` script in a real shell and records the result. Commit the tape next to the output, so anyone can run it again after the CLI changes.

```elixir
Output assets/demo-dark.gif

Require mytool
Set Theme "GitHub Dark"
Set FontSize 16
Set Width 1000
Set Height 520
Set Padding 24

Hide
Type "cd examples/basic && clear"
Enter
Show

Type "mytool sync --dry-run"
Sleep 400ms
Enter
Wait /done/
Sleep 3s
```

- `Hide` and `Show` keep setup steps out of the recording.
- `Wait /regex/` waits until the output matches, instead of guessing a `Sleep` long enough for slow commands.
- `Require` fails early if the binary isn't on `PATH`.
- For light and dark, keep the commands in 1 tape and `Source` it from 2 small tapes that only set `Output` and `Theme`. VHS ships `GitHub Dark` and `Github` for the 2 GitHub themes.
- End with a `Sleep` of 2 to 3 seconds, so the final state stays on screen before the GIF loops.
- VHS needs `ttyd` and `ffmpeg`. In CI, [vhs-action](https://github.com/charmbracelet/vhs-action) can regenerate the GIFs on every release.

## asciinema

Use asciinema when the session is easier to type live than to script, or when it depends on timing you can't predict.

```sh
asciinema rec demo.cast
agg --theme github-dark demo.cast assets/demo-dark.gif
agg --theme github-light demo.cast assets/demo-light.gif
```

- 1 recording gives both themes. Render it twice.
- Edit pauses and typos out of the `.cast` before rendering. It's a JSON lines file, 1 event per line.
- Use agg's idle time limit to cut long pauses down without editing the file.

## Screen recordings

For GUI and web apps:

- Record only the app window, at the size it will appear in the README.
- Convert with gifski. `--fps 15` and a `--width` near the display width keep the file small.
- If the app has a dark mode, record it twice and switch with `<picture>`. See [Light and dark](light-and-dark.md).

## Video

- GitHub plays MP4, MOV and WebM in a README only from an uploaded attachment, not from a file in the repo. Drag the file into GitHub's README editor or an issue, then paste the `user-attachments` URL on its own line.
- The limit is 10 MB on free plans and 100 MB on paid ones. Encode with H.264 so every browser plays it.
- A video doesn't autoplay. It works for a walkthrough further down, not for the demo under the header.
- npm, crates.io and most other registries don't play it. Put a GIF or a screenshot first if the README is published there.

## Keep it small

- 10 to 20 seconds. Show 1 task from start to finish, not every feature.
- Size the terminal to the content. Empty rows and columns cost bytes and shrink the text.
- Anything over a few MB loads slowly. If a GIF gets that big, cut it or switch to a video.
- A GIF ignores `prefers-reduced-motion` and can't be paused. Give it an `alt` that describes what happens.
