# Badges

[shields.io](https://shields.io) draws a badge from its URL. Change the URL, get a different badge. Nothing to host, nothing to build.

Every badge here uses the `for-the-badge` style. It's taller, uppercase and square, so a row of them reads as a set of buttons rather than stickers.

## Styles

Same badge, 5 styles:

| Style | Badge |
| :--- | :---: |
| `flat` (default) | ![flat][style-flat] |
| `flat-square` | ![flat-square][style-flat-square] |
| `plastic` | ![plastic][style-plastic] |
| `for-the-badge` | ![for-the-badge][style-for-the-badge] |
| `social` | ![social][style-social] |

`flat` is what most READMEs ship. `social` only looks right for stars and followers. `plastic` has a gradient from 2014.

## Anatomy

A static badge puts label, message and color in the path:

```
https://img.shields.io/badge/<label>-<message>-<color>?style=for-the-badge
```

Escaping in the path:

| To get | Write |
| :---: | :---: |
| a space | `_` or `%20` |
| `-` | `--` |
| `_` | `__` |
| `≥` | `%E2%89%A5` |

Write `≥` and `≤` as single characters, not `>=` and `<=`. They read cleaner in uppercase on a narrow badge.

Query parameters that work on every badge:

| Parameter | Does |
| :--- | :--- |
| `style` | One of the 5 styles above |
| `label` | Overrides the left text. Empty hides it |
| `color` | Right side. Hex without `#`, or a named color |
| `labelColor` | Left side |
| `logo` | A [Simple Icons](https://simpleicons.org) slug, or a data URI |
| `logoColor` | Recolors a Simple Icons logo. No effect on data URIs |
| `cacheSeconds` | How long GitHub's image proxy keeps it. Raise it for slow APIs |

## Types

### Static

The text is in the URL. Use it for facts that change by hand, like a minimum runtime version.

![node][static-node]

```
https://img.shields.io/badge/node-%E2%89%A524-00A4EF?style=for-the-badge&logo=nodedotjs&logoColor=white
```

### Service

Shields.io knows the API of GitHub, npm, crates.io, PyPI and a few hundred more. Name the service and the repo or package, and it fetches the value.

| Badge | Path |
| :---: | :--- |
| ![last commit][svc-commit] | `github/last-commit/<owner>/<repo>` |
| ![license][svc-license] | `github/license/<owner>/<repo>` |
| ![npm][svc-npm] | `npm/v/<package>` |
| ![ci][svc-ci] | `github/actions/workflow/status/<owner>/<repo>/<file>.yml` |

Browse the full list on [shields.io](https://shields.io/badges).

### Dynamic JSON

For an API shields.io doesn't know. Give it a URL and a [JSONPath](https://jsonpath.com) query, and it prints whatever the query returns. There are `dynamic/yaml`, `dynamic/xml` and `dynamic/toml` variants too.

![version][dyn-version]

```
https://img.shields.io/badge/dynamic/json
  ?url=<url-encoded API URL>
  &query=%24.latestVersion.version
  &prefix=v
  &label=clawhub
  &style=for-the-badge
```

`prefix` and `suffix` wrap the value, so `0.0.4` becomes `v0.0.4`.

### Endpoint

The API returns the whole badge as JSON, and shields.io draws it. Use it when you control the API or the service already exposes one.

![installs][endpoint-installs]

```json
{
  "schemaVersion": 1,
  "label": "installs",
  "message": "2",
  "color": "0a0a0a"
}
```

```
https://img.shields.io/endpoint?url=<url-encoded JSON URL>&style=for-the-badge
```

Query parameters override the JSON. That's how the badge above gets `for-the-badge` and a new label even though the service sends `flat`.

## Gallery

### Theme palette

Take the colors from the project's banner or editor theme, 1 per badge. This set is [Tokyo Night](https://github.com/tokyo-night/tokyo-night-vscode-theme), the same as this repo's banner.

![skill][tn-skill]
![commit][tn-commit]
![license][tn-license]
![ci][tn-ci]
![issues][tn-issues]

`9854f1` `7aa2f7` `e0af68` `9ece6a` `f7768e`

### Brand palette

A brand with 4 colors gets 1 per badge. It reads as a logo split across the row.

![ci][brand-ci]
![license][brand-license]
![node][brand-node]
![npm][brand-npm]

`7FBA00` `FFB900` `00A4EF` `F25022`

### Dark label

Set `labelColor` to the theme background and keep the accent on the message. Quieter than full color, and the logo pops.

![version][dark-version]
![license][dark-license]
![node][dark-node]

```
&labelColor=1a1b26&color=7aa2f7&logoColor=7aa2f7
```

### Stack chips

Drop the label and put a logo on the message. Good for a "built with" row. Use the brand's own color.

![TypeScript][chip-ts]
![Rust][chip-rust]
![Python][chip-python]
![Bun][chip-bun]

```
https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white
```

### Logo only

Empty label, empty message. A square button for a link that needs no words.

![GitHub][logo-github]
![npm][logo-npm]
![Discord][logo-discord]

```
https://img.shields.io/badge/-1a1b26?style=for-the-badge&logo=github&logoColor=white
```

## Custom badges

Shields.io has no service for most new registries. Dynamic JSON plus your own logo gets a badge that looks native.

![version][claw-version]
![downloads][claw-downloads]

The recipe:

1. Find the registry's public API and the JSONPath to the value. `curl` it and look.
2. Use `dynamic/json` with `prefix=v` for versions.
3. Take the registry's brand color for `color`, and a neutral gray for `labelColor`.
4. Embed the registry's logo as a data URI, since Simple Icons won't have it.

### Embed a logo

`logo` accepts a base64 data URI. SVG keeps it small. A 28 × 28 PNG works if there's no SVG.

```sh
printf 'data:image/png;base64,%s' "$(base64 -w0 logo.png)" | jq -sRr @uri
```

Paste the output after `logo=`.

- `logoColor` doesn't recolor it. Bake the color you want into the file.
- Keep it under 3 KB. The whole URL goes into the README and into GitHub's image proxy.
- Put the URL in a reference link at the bottom of the file, so the header stays readable.

## Markup

Badges go in the centered header block. Use reference links, so each line in the header is short:

```markdown
[![Last commit][commit-badge]][commits]
[![License][license-badge]][license]

[commits]: https://github.com/<owner>/<repo>/commits/main
[license]: LICENSE

[commit-badge]: https://img.shields.io/github/last-commit/<owner>/<repo>?style=for-the-badge&color=7aa2f7
[license-badge]: https://img.shields.io/github/license/<owner>/<repo>?style=for-the-badge&color=e0af68
```

- Link every badge somewhere useful: the CI badge to the workflow, the version badge to the registry page.
- 3 to 5 badges in the header. Put install-specific ones, like runtime version or package version, in the install section.

## Avoid

- Mixing styles in one row.
- The default `brightgreen` and `blue`. They match nothing.
- White or near-white badges. They vanish on GitHub's light theme.
- Badges that say nothing, like "made with love" or "PRs welcome".
- Hand-written version numbers in static badges. They go stale. Use a service or dynamic badge.

<!----------------------------------------------------------------------------->

[style-flat]: https://img.shields.io/badge/license-MIT-e0af68?style=flat
[style-flat-square]: https://img.shields.io/badge/license-MIT-e0af68?style=flat-square
[style-plastic]: https://img.shields.io/badge/license-MIT-e0af68?style=plastic
[style-for-the-badge]: https://img.shields.io/badge/license-MIT-e0af68?style=for-the-badge
[style-social]: https://img.shields.io/github/stars/shbernal/awesome-readme?style=social

[static-node]: https://img.shields.io/badge/node-%E2%89%A524-00A4EF?style=for-the-badge&logo=nodedotjs&logoColor=white

[svc-commit]: https://img.shields.io/github/last-commit/shbernal/awesome-readme?style=for-the-badge&color=7aa2f7
[svc-license]: https://img.shields.io/github/license/shbernal/awesome-readme?style=for-the-badge&color=e0af68
[svc-npm]: https://img.shields.io/npm/v/charcheck?style=for-the-badge&color=CB3837&logo=npm&logoColor=white
[svc-ci]: https://img.shields.io/github/actions/workflow/status/shbernal/ooxml-ai-tooling/ci.yml?branch=main&style=for-the-badge&label=CI&color=9ece6a

[dyn-version]: https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fclawhub.ai%2Fapi%2Fv1%2Fskills%2Fooxml-lookup&query=%24.latestVersion.version&prefix=v&label=clawhub&style=for-the-badge

[endpoint-installs]: https://img.shields.io/endpoint?url=https%3A%2F%2Fwww.skills.sh%2Fapi%2Fbadge%2Fshbernal%2Fawesome-readme&style=for-the-badge&label=installs

[tn-skill]: https://img.shields.io/badge/agent_skill-awesome--readme-9854f1?style=for-the-badge
[tn-commit]: https://img.shields.io/github/last-commit/shbernal/awesome-readme?style=for-the-badge&color=7aa2f7
[tn-license]: https://img.shields.io/github/license/shbernal/awesome-readme?style=for-the-badge&color=e0af68
[tn-ci]: https://img.shields.io/badge/CI-passing-9ece6a?style=for-the-badge
[tn-issues]: https://img.shields.io/github/issues/shbernal/awesome-readme?style=for-the-badge&color=f7768e

[brand-ci]: https://img.shields.io/badge/CI-passing-7FBA00?style=for-the-badge
[brand-license]: https://img.shields.io/badge/license-MIT-FFB900?style=for-the-badge
[brand-node]: https://img.shields.io/badge/node-%E2%89%A524-00A4EF?style=for-the-badge&logo=nodedotjs&logoColor=white
[brand-npm]: https://img.shields.io/badge/npm-v1.2.0-F25022?style=for-the-badge&logo=npm&logoColor=white

[dark-version]: https://img.shields.io/badge/version-v1.2.0-CB3837?style=for-the-badge&labelColor=1a1b26&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI0NCMzgzNyIgZD0iTTEuNzYzIDBDLjc4NiAwIDAgLjc4NiAwIDEuNzYzdjIwLjQ3NEMwIDIzLjIxNC43ODYgMjQgMS43NjMgMjRoMjAuNDc0Yy45NzcgMCAxLjc2My0uNzg2IDEuNzYzLTEuNzYzVjEuNzYzQzI0IC43ODYgMjMuMjE0IDAgMjIuMjM3IDB6Ii8%2BPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTUuMTMgNS4zMjNsMTMuODM3LjAxOS0uMDA5IDEzLjgzNmgtMy40NjRsLjAxLTEwLjM4MmgtMy40NTZMMTIuMDQgMTkuMTdINS4xMTN6Ii8%2BPC9zdmc%2BCg%3D%3D
[dark-license]: https://img.shields.io/badge/license-MIT-e0af68?style=for-the-badge&labelColor=1a1b26&logo=opensourceinitiative&logoColor=e0af68
[dark-node]: https://img.shields.io/badge/node-%E2%89%A524-9ece6a?style=for-the-badge&labelColor=1a1b26&logo=nodedotjs&logoColor=9ece6a

[chip-ts]: https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white
[chip-rust]: https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white
[chip-python]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[chip-bun]: https://img.shields.io/badge/Bun-14151A?style=for-the-badge&logo=bun&logoColor=fbf0df

[logo-github]: https://img.shields.io/badge/-1a1b26?style=for-the-badge&logo=github&logoColor=white
[logo-npm]: https://img.shields.io/badge/-CB3837?style=for-the-badge&logo=npm&logoColor=white
[logo-discord]: https://img.shields.io/badge/-5865F2?style=for-the-badge&logo=discord&logoColor=white

[claw-version]: https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fclawhub.ai%2Fapi%2Fv1%2Fskills%2Fooxml-lookup&query=%24.latestVersion.version&prefix=v&label=clawhub&labelColor=555555&style=for-the-badge&color=F5654A&logo=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgoAAAANSUhEUgAAABwAAAAcCAYAAAByDd%2BUAAAG%2BklEQVRIx22WW4idVxXHf2vt%2FZ37mcuZdHKZpM29iQZEWoRiqb1QKFotKlRbaPVV%2B%2BaLRbC%2B9kH0QfC94AWhoFQUhaIUq0FL2wltY5qmmUkmmcxMZpK55HzfOd%2F37b18ODNnZmw3LDh8rLP%2F67%2F3f%2F33EoBDBw7Q6%2FVxztFNU7751afk72%2F8rdHLMgVBVRBVBAEBEQHAzBgu2%2F5Rq9fj0089lf7ylVes1WxRlCXHWm3Ozl5GvnDffbw7PU2j0aDVajV6We8JM%2FuyYEcwEkRwqgNAEQZYws5lZjsiAhQgM4j8uV6v%2F6WbdtOs12Oi00FajSYCJIk%2FUJThZTN7GrMqCE4MVcHE4dQNmG6y2ySLGcRohBhRAhaNIoIMTqKvqr%2BrVio%2FLMpyATN8pVLBqTbSLHs5xviciNBKjEeOCt6XLK0a4j3nVxK6ueJUdjA0QjTa1chn7iqJRcFkS3Dqef1jWO1LVUJ4PoQQW83mC2UZUhdDJMT4ZBnKnwC%2BIZFv7yt54ajw3o2SvaNVHhiH%2BycKLmXCajqgZTZgdWjUeOF4yZGKEZzC7ZIfHBa0V3J%2BA3oRzOKpEOJ0r9%2B%2FoI8%2B%2FCUNITxp0apqxr2U3L0Ymb9SkBeRx08kHD%2FaIV0p%2Bd7xkk4rEswIZtzVNr5%2FFG4t5pw8PsYTJxyaR%2BZnSw7OR87EEo2REGKtDOWXf%2Fzii6LvnDtXM7O7oxkdCzT7kZkU5u4Y1apwsppz0nve7XuWFguePmX4RPAJfOOEcfF6xnSpnKpUOO0H%2F%2Flww3ivZ7h%2BZCJGohmhDPf89Oc%2Fq2kZgpiZAoxiLAEzGJcy47TC5Fs5%2FdkUU3h1SZgkZ2oCpjowEnJeu2W4BPK5HpPv9Dnh4ULXuBjhGtCWuKVkX4agfkvaAqiH2wF6BnvX4PAanKvAh5V1lrPAXE95a77k1GiOYUwvB5Zyz0oa%2BNfyGkevgfWNFYOrQC4w5kCCIepotVp4NpvXgNCAkQjXcjjbh3UxFg5FrmQ5s%2BuOQ21Ql9C83keAtJNwcAyu3BH%2B0cq5NAkXLsMHBsvAQQdFAlYyFJnudIrVIIzsEVoCEViqwEdiXEwFnHFvR%2FjaY4c4saGcTh2PPrCPY20jKlzoCh9hLCQQgLbASEdYQ7FNc%2BhnGX7oTmIsd4XRpnB8LywtGMcK%2BOKo8vqooD1j4aOcuflZHsoiTuCNV6%2BznAamOsr%2BSXjIhDdnjDtA5y646ZSVniCbvici6I4exhAu33TQFCojcDHC4nljdCXi70QqBUysBk4anIwwtRbRAmwjMn7LWPivMRPBN0Hqysyy7rJA9R4%2FwLIhqplyftnx4DFYmI%2F8%2FrZRvQb9OLjnDWBtM%2FsGxgqQZPD%2BVaOr0JqAqUnh7HXFTIaurqo0mk12l2AgYqylwhuXHPsPKY8%2FIDQnwcWBEN4GPjBj2uCfwDpQEWjvgcc%2FLxw4qLw551jPFJFtU98C9kMzHjo%2FqMJGT3l7Fo6cCIzXoRDjWA069wjdcaUA9t6KHLtqhBz2NAQX4N1ryp2%2BQzB2vV5mFHmO2rAttqoYJKrAcleYi7BvHPyYkOYQrxunbxgnb0CYN7J8cGcTozCvws1UUfnEI0mMke7GBmoMcbBhDI6hKIX%2FXFGoQhiD%2BhjcFJipweVa5LaH5tigGKnD2TmlLHe%2BjztBBfVu0PjG%2F69Bsggs3BJ%2BPS10%2B%2FDZEbCKsXTHyBWkAquF8OEN4dxtyPr6yZ1s8%2FQMYhnwnwIFtvWyQzRhI1VMDF%2BHEQXXFlBobBjOCeWqsJ4KTndPAEN2BqKCT5LtO9wG22K4GRgVhftHjWcDTBTQzw3rGXdnwncU7t9jVOSTYLtFE8myFHWqJhC3wRgmmhlqxj6LNNcjyzeNmocHF%2BChRWhUYP2GMbIWmbKIfArYFiERKWu1evSPPfJw9ofX%2FnhFogxZCjJIFKgadMz4OMBSxZhagY10UNuFAq4JrPVhUo1FIimyo%2FBtiqI6%2B9KPXuqJUyVJkq8XRfFbjOr2gDQoQIGjEpkAet5YKaEMA3OveRj3UC%2BFFRM%2BRoi2W3ib%2B%2FWSJPlWURSvuZFWm2qlerUsyiNm9rlhRVuzJ3ALYQmh54WJMdCmUG1AvS7Ml47ZUrhpskvtO%2B%2FPeferZqP5i8T70qlTiiIvksT%2F28wmDU7BQL07Z9AokEXldk%2FpB6GbK4upkJZC%2FJSW2iy677z7Tb1efzHP89UQInJmcpL3l5aoVSo0W61GlmVPhDJ8JcZ42CwmW4DbDiiDDWXnOGzs0BwiUqjqjHPuT41G469pmqa9fp%2F9B%2FYPEg6eOUOjVmN0ZASvjmeeeVbH2u1mzfv2VtS3wvl2zfl23bnNb0m77gbf696360nSHmu1m9997nnx6hgfHaXZaHDk8GEA%2FgcKL8ikX%2BEcEAAAAABJRU5ErkJggg%3D%3D
[claw-downloads]: https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fclawhub.ai%2Fapi%2Fv1%2Fskills%2Fooxml-lookup&query=%24.skill.stats.downloads&label=downloads&labelColor=555555&style=for-the-badge&color=F5654A&logo=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgoAAAANSUhEUgAAABwAAAAcCAYAAAByDd%2BUAAAG%2BklEQVRIx22WW4idVxXHf2vt%2FZ37mcuZdHKZpM29iQZEWoRiqb1QKFotKlRbaPVV%2B%2BaLRbC%2B9kH0QfC94AWhoFQUhaIUq0FL2wltY5qmmUkmmcxMZpK55HzfOd%2F37b18ODNnZmw3LDh8rLP%2F67%2F3f%2F33EoBDBw7Q6%2FVxztFNU7751afk72%2F8rdHLMgVBVRBVBAEBEQHAzBgu2%2F5Rq9fj0089lf7ylVes1WxRlCXHWm3Ozl5GvnDffbw7PU2j0aDVajV6We8JM%2FuyYEcwEkRwqgNAEQZYws5lZjsiAhQgM4j8uV6v%2F6WbdtOs12Oi00FajSYCJIk%2FUJThZTN7GrMqCE4MVcHE4dQNmG6y2ySLGcRohBhRAhaNIoIMTqKvqr%2BrVio%2FLMpyATN8pVLBqTbSLHs5xviciNBKjEeOCt6XLK0a4j3nVxK6ueJUdjA0QjTa1chn7iqJRcFkS3Dqef1jWO1LVUJ4PoQQW83mC2UZUhdDJMT4ZBnKnwC%2BIZFv7yt54ajw3o2SvaNVHhiH%2BycKLmXCajqgZTZgdWjUeOF4yZGKEZzC7ZIfHBa0V3J%2BA3oRzOKpEOJ0r9%2B%2FoI8%2B%2FCUNITxp0apqxr2U3L0Ymb9SkBeRx08kHD%2FaIV0p%2Bd7xkk4rEswIZtzVNr5%2FFG4t5pw8PsYTJxyaR%2BZnSw7OR87EEo2REGKtDOWXf%2Fzii6LvnDtXM7O7oxkdCzT7kZkU5u4Y1apwsppz0nve7XuWFguePmX4RPAJfOOEcfF6xnSpnKpUOO0H%2F%2Flww3ivZ7h%2BZCJGohmhDPf89Oc%2Fq2kZgpiZAoxiLAEzGJcy47TC5Fs5%2FdkUU3h1SZgkZ2oCpjowEnJeu2W4BPK5HpPv9Dnh4ULXuBjhGtCWuKVkX4agfkvaAqiH2wF6BnvX4PAanKvAh5V1lrPAXE95a77k1GiOYUwvB5Zyz0oa%2BNfyGkevgfWNFYOrQC4w5kCCIepotVp4NpvXgNCAkQjXcjjbh3UxFg5FrmQ5s%2BuOQ21Ql9C83keAtJNwcAyu3BH%2B0cq5NAkXLsMHBsvAQQdFAlYyFJnudIrVIIzsEVoCEViqwEdiXEwFnHFvR%2FjaY4c4saGcTh2PPrCPY20jKlzoCh9hLCQQgLbASEdYQ7FNc%2BhnGX7oTmIsd4XRpnB8LywtGMcK%2BOKo8vqooD1j4aOcuflZHsoiTuCNV6%2BznAamOsr%2BSXjIhDdnjDtA5y646ZSVniCbvici6I4exhAu33TQFCojcDHC4nljdCXi70QqBUysBk4anIwwtRbRAmwjMn7LWPivMRPBN0Hqysyy7rJA9R4%2FwLIhqplyftnx4DFYmI%2F8%2FrZRvQb9OLjnDWBtM%2FsGxgqQZPD%2BVaOr0JqAqUnh7HXFTIaurqo0mk12l2AgYqylwhuXHPsPKY8%2FIDQnwcWBEN4GPjBj2uCfwDpQEWjvgcc%2FLxw4qLw551jPFJFtU98C9kMzHjo%2FqMJGT3l7Fo6cCIzXoRDjWA069wjdcaUA9t6KHLtqhBz2NAQX4N1ryp2%2BQzB2vV5mFHmO2rAttqoYJKrAcleYi7BvHPyYkOYQrxunbxgnb0CYN7J8cGcTozCvws1UUfnEI0mMke7GBmoMcbBhDI6hKIX%2FXFGoQhiD%2BhjcFJipweVa5LaH5tigGKnD2TmlLHe%2BjztBBfVu0PjG%2F69Bsggs3BJ%2BPS10%2B%2FDZEbCKsXTHyBWkAquF8OEN4dxtyPr6yZ1s8%2FQMYhnwnwIFtvWyQzRhI1VMDF%2BHEQXXFlBobBjOCeWqsJ4KTndPAEN2BqKCT5LtO9wG22K4GRgVhftHjWcDTBTQzw3rGXdnwncU7t9jVOSTYLtFE8myFHWqJhC3wRgmmhlqxj6LNNcjyzeNmocHF%2BChRWhUYP2GMbIWmbKIfArYFiERKWu1evSPPfJw9ofX%2FnhFogxZCjJIFKgadMz4OMBSxZhagY10UNuFAq4JrPVhUo1FIimyo%2FBtiqI6%2B9KPXuqJUyVJkq8XRfFbjOr2gDQoQIGjEpkAet5YKaEMA3OveRj3UC%2BFFRM%2BRoi2W3ib%2B%2FWSJPlWURSvuZFWm2qlerUsyiNm9rlhRVuzJ3ALYQmh54WJMdCmUG1AvS7Ml47ZUrhpskvtO%2B%2FPeferZqP5i8T70qlTiiIvksT%2F28wmDU7BQL07Z9AokEXldk%2FpB6GbK4upkJZC%2FJSW2iy677z7Tb1efzHP89UQInJmcpL3l5aoVSo0W61GlmVPhDJ8JcZ42CwmW4DbDiiDDWXnOGzs0BwiUqjqjHPuT41G469pmqa9fp%2F9B%2FYPEg6eOUOjVmN0ZASvjmeeeVbH2u1mzfv2VtS3wvl2zfl23bnNb0m77gbf696360nSHmu1m9997nnx6hgfHaXZaHDk8GEA%2FgcKL8ikX%2BEcEAAAAABJRU5ErkJggg%3D%3D
