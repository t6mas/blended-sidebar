# Blended Sidebar

Applies the same page-aware adaptive color that **[Blended Addressbar](https://github.com/kkugot/blended-addressbar)** uses on the URL bar to the left sidebar icon strip.

<p align="center">
  <img src="https://i.postimg.cc/38nJFsPN/204shots-so.png" alt="Blended Sidebar Preview" width="100%">
</p>

## Requirements

**[Blended Addressbar](https://github.com/kkugot/blended-addressbar) must be installed and enabled.** This mod only adds CSS — it reuses the `--zen-tab-header-background` and `--zen-tab-header-foreground` variables that the blended-addressbar's script writes on every tab change.

## Installation

There are two ways to install this mod using Sine.

### Method 1: Easy Install (Recommended)
1. Open Zen Browser **Settings**.
2. Go to the **Sine mods** section.
3. Scroll down to the input box under *"or, add your own locally from a GitHub repo."*
4. Paste the URL of this repository and click add.
5. Enable **Blended Sidebar** in the Sine settings and restart Zen.

### Method 2: Manual Install
If the easy install fails, you can add it manually:
1. Open your Zen Browser profile folder (e.g., `C:\Users\YourUser\AppData\Roaming\zen\Profiles\[your-profile]\chrome\sine-mods\`).
2. Copy the `blended-sidebar` folder into the `sine-mods` directory.
3. Open the `mods.json` file located in the `sine-mods` folder and carefully paste the following configuration inside the main object (don't forget the comma if it's not the first item):

```json
"blended-sidebar": {
  "id": "blended-sidebar",
  "name": "Blended Sidebar",
  "description": "A page-aware sidebar that adapts its color to match the active website.",
  "author": "based on blended-addressbar by kkugot",
  "version": "1.0.0",
  "updatedAt": "2026-05-09",
  "tags": ["sidebar", "adaptive", "theming", "zen browser"],
  "fork": ["zen"],
  "scripts": {
    "blended-sidebar.uc.js": {
      "include": ["chrome://browser/content/browser.xhtml"]
    }
  },
  "style": {
    "chrome": "style.css",
    "content": ""
  },
  "readme": "README.md",
  "js": true,
  "createdAt": "2026-05-09",
  "no-updates": true,
  "enabled": true
}
