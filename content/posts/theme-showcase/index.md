+++
title = "Theme showcase: all markdown features"
summary = "A reference post that demonstrates every text block the VnG Blue theme renders — headings, lists, code, tables, blockquotes, images, and inline formatting. Use it as a visual checklist when tweaking the theme."
date = "2025-03-01T10:39:08+01:00"
draft = false
categories = [
  "My awesome category"
]
tags = [
  "showcase",
  "markdown",
  "reference"
]
+++

This post exists for one reason: to show how every markdown element looks once the VnG Blue theme has rendered it. Each section below is a single block type. If you change typography, colors, or spacing in the theme, this is the page to open first.

## Inline formatting

Most of what readers see is just running prose. The theme leans on its **Montserrat** body font for paragraphs and a mono **Geist Mono** face for anything code-shaped. Inside a sentence you have **bold for emphasis**, *italics for tone*, ~~strikethrough for retractions~~, and `inline code` for filenames like `~/.config/hypr/hyprland.conf`.

Links should stand out without shouting — visit the [Hugo documentation](https://gohugo.io/documentation/) to see the underline treatment in context. Keyboard chords use the <kbd>kbd</kbd> element, e.g. press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> to open the command palette.

## Headings

The theme styles all six heading levels. They share the secondary mono face and the link-blue color, with size as the only signal of hierarchy.

# Heading level 1

## Heading level 2

### Heading level 3

#### Heading level 4

##### Heading level 5

###### Heading level 6

## Paragraphs

A post is mostly paragraphs, so the body line-height matters more than any single decorative block. Two short paragraphs follow — enough to judge measure, leading, and the rhythm between blocks.

Hugo is a static site generator written in Go. It takes a directory of Markdown files and a theme, then produces a fully static site you can host anywhere — GitHub Pages, Netlify, Cloudflare Pages, or a tiny VPS running nginx. There is no database, no PHP, no Node runtime in production.

The trade-off is that everything happens at build time. Want a comment section, search, or analytics? You wire in a third-party service or generate the index ahead of time. In return you get sub-second page loads and a deploy artifact you could, in principle, keep on a USB stick.

## Blockquote

> A user interface is like a joke. If you have to explain it, it's not that good.

Longer quotes carry attribution on a separate line:

> Premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%.
>
> — Donald Knuth, *Structured Programming with go to Statements*, 1974

## Lists

Unordered list with a nested level:

- Window manager
  - Hyprland (Wayland)
  - i3 (X11)
- Status bar
  - Waybar
  - Polybar
- Launcher
  - Wofi
  - Rofi

Ordered list, used for genuine sequence:

1. Install Hugo and Go.
2. Run `hugo new site my-blog`.
3. Add the theme as a Hugo module.
4. Write your first post under `content/posts/`.
5. Run `hugo server -D` and open `http://localhost:1313`.

## Code blocks

Syntax highlighting uses Hugo's `friendly` style. A few common languages:

```bash
#!/usr/bin/env bash
set -euo pipefail

for post in content/posts/*/index.md; do
  echo "Found: $post"
done
```

```python
from pathlib import Path

def count_posts(root: Path) -> int:
    return sum(1 for _ in root.glob("posts/*/index.md"))

print(count_posts(Path("content")))
```

```yaml
baseURL: "https://example.com/"
languageCode: en-US
title: My Blog
theme:
  - github.com/ismd/hugo-theme-vng-blue
params:
  description: "A small blog about big ideas."
```

## Table

| Component   | Tool       | Config file                         |
|-------------|------------|-------------------------------------|
| Compositor  | Hyprland   | `~/.config/hypr/hyprland.conf`      |
| Status bar  | Waybar     | `~/.config/waybar/config.jsonc`     |
| Launcher    | Wofi       | `~/.config/wofi/config`             |
| Terminal    | Kitty      | `~/.config/kitty/kitty.conf`        |
| Lock screen | Hyprlock   | `~/.config/hypr/hyprlock.conf`      |

## Horizontal rule

Section breaks use a thematic break:

---

Anything above the rule is visually closed off from anything below it.

## Image

Inline images use standard markdown. The cover image of this post, rendered inside the body:

![Theme cover illustration](cover.png)

That's the full set. If a future markdown element is added to the theme — admonitions, footnotes, definition lists — it should show up here too.
