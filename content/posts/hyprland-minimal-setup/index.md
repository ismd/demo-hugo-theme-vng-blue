+++
title = "Hyprland: my minimal setup for a daily-driver Wayland desktop"
summary = "After a year of running Hyprland as my only desktop, here is the smallest config that still feels like home — window rules, keybindings, Waybar, and a few decisions I would not change."
date = "2025-02-10T09:15:00+01:00"
draft = false
categories = [
  "Linux"
]
tags = [
  "hyprland",
  "wayland",
  "linux",
  "ricing"
]
+++

> ## Demo post — not real content
>
> **This article is a placeholder that exists to demonstrate how the [VnG Blue Hugo theme](https://github.com/ismd/hugo-theme-vng-blue) renders a typical technical write-up.** The Hyprland configuration shown below is illustrative; it is not a real personal setup and should not be copied verbatim.

I switched to Hyprland a year ago and never went back. It is fast, it is Wayland-native, and the config file reads like a tiny DSL instead of a maze of GNOME settings. This post is the minimal version of what I actually run — no fifty-line shadow tweaks, no thirty animated workspaces, just the parts that earn their place every day.

## What you need

A short shopping list. Everything below is available in the Arch repos or the AUR:

- `hyprland` — the compositor itself
- `waybar` — top status bar
- `wofi` — application launcher
- `kitty` — terminal emulator
- `hyprlock` and `hypridle` — lock screen and idle daemon
- `grim` + `slurp` — screenshots
- `wl-clipboard` — clipboard utilities

I avoid the all-in-one ricing packs. They give you a beautiful screenshot and a config you do not understand.

## Window rules

Hyprland's rule syntax is one of the reasons I stayed. You match by `class`, `title`, or both, and apply behavior declaratively:

```ini
# Float dialogs and pickers
windowrulev2 = float, class:^(pavucontrol)$
windowrulev2 = float, class:^(nm-connection-editor)$
windowrulev2 = float, title:^(Open File)$

# Keep media on workspace 5
windowrulev2 = workspace 5 silent, class:^(Spotify)$
windowrulev2 = workspace 5 silent, class:^(mpv)$

# No shadow on tiled terminals
windowrulev2 = noshadow, class:^(kitty)$
```

> **Tip.** Run `hyprctl clients` to see the exact `class` and `title` strings of every open window. Half the time a rule fails because the regex matches an empty string.

## Keybindings

I keep one modifier — <kbd>SUPER</kbd> — and resist the urge to add chord prefixes. Muscle memory is the whole point.

| Binding                          | Action                  |
|----------------------------------|-------------------------|
| <kbd>SUPER</kbd>+<kbd>Q</kbd>    | Launch terminal         |
| <kbd>SUPER</kbd>+<kbd>D</kbd>    | Open Wofi launcher      |
| <kbd>SUPER</kbd>+<kbd>W</kbd>    | Close active window     |
| <kbd>SUPER</kbd>+<kbd>F</kbd>    | Toggle fullscreen       |
| <kbd>SUPER</kbd>+<kbd>V</kbd>    | Toggle floating         |
| <kbd>SUPER</kbd>+<kbd>1..9</kbd> | Switch workspace        |
| <kbd>SUPER</kbd>+<kbd>SHIFT</kbd>+<kbd>1..9</kbd> | Move window to workspace |
| <kbd>SUPER</kbd>+<kbd>L</kbd>    | Lock screen             |

The corresponding section in `hyprland.conf` is just:

```ini
$mod = SUPER
$term = kitty
$menu = wofi --show drun

bind = $mod, Q, exec, $term
bind = $mod, D, exec, $menu
bind = $mod, W, killactive
bind = $mod, F, fullscreen, 0
bind = $mod, V, togglefloating
bind = $mod, L, exec, hyprlock

# Workspaces 1..9
bind = $mod, 1, workspace, 1
bind = $mod SHIFT, 1, movetoworkspace, 1
# ...repeat for 2..9
```

## Status bar

Waybar covers the bar. My config is a single JSONC file, and the modules I keep are: workspaces, window title, clock, network, audio, battery. That is it. No weather widget I never look at.

```jsonc
{
  "layer": "top",
  "position": "top",
  "height": 28,
  "modules-left": ["hyprland/workspaces", "hyprland/window"],
  "modules-center": ["clock"],
  "modules-right": ["pulseaudio", "network", "battery"],

  "clock": {
    "format": "{:%a %d %b  %H:%M}"
  },
  "battery": {
    "format": "{capacity}% {icon}",
    "format-icons": ["", "", "", "", ""]
  }
}
```

The CSS is even shorter — match your theme accent, set a readable monospace font, ship it.

## What I would skip

A short list of things I tried and removed:

1. **Heavy blur and shadow.** Pretty in screenshots, distracting during work.
2. **Animated workspace switches above 200&nbsp;ms.** Anything longer feels broken once you do it a hundred times a day.
3. **A second status bar at the bottom.** Twice the maintenance for half the information density.
4. **Dynamic wallpapers tied to the time of day.** Cute for a week.

## Wrap-up

The full dotfiles live in a small public repo — `git clone` it, read the four files, copy what you want. If something here looks too opinionated, that is fine: a desktop you have not customized is a desktop you do not own.

If you are still on the fence, give it a weekend. Wayland is no longer the future. It is the present.
