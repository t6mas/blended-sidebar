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
4. Paste the URL of this repository and click **Add**.
5. Enable **Blended Sidebar** in the Sine settings and restart Zen Browser.

### Method 2: Manual Install
If the easy install fails, you can add it manually:
1. Open your Zen Browser profile folder (e.g., `C:\Users\YourUser\AppData\Roaming\zen\Profiles\[your-profile]\chrome\sine-mods\`).
2. Copy the `blended-sidebar` folder into the `sine-mods` directory.
3. Open the `mods.json` file located in the `sine-mods` folder.
4. Carefully paste the following configuration inside the main object (don't forget to add a comma before it if it's not the first item):

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
```

5. Reload Sine or restart Zen Browser.

## Disclaimer & Compatibility

Please note that this mod has undergone limited testing and might contain bugs. It targets Zen Browser dual-toolbar layouts. Compact mode is supported, but visual validation is still recommended after Zen updates because browser UI selectors can change. Feel free to report any issues!

---

## 🛠️ Bonus: My Blended Addressbar Fixes (Compact Mode)

If you are using the original Blended Addressbar mod and experiencing squished icons pushed to the left, or a "floating" loading line when using **Compact Mode**, I have tweaked some of the original CSS to fix these layout issues.

<details>
<summary><b>Click here to view my fixed files for Blended Addressbar</b></summary>

<br>

Replace the code at the very end of your original `blended-addressbar/style.css` with this to restore vertical padding without breaking the horizontal layout:

```css
:root:not([zen-single-toolbar="true"]) {
  #zen-appcontent-wrapper {
    margin-left: 0 !important;
    margin-right: 0 !important;
  }

  #nav-bar {
    padding-block: 0 !important;
  }
}
```

Replace the compact mode section in your original `blended-addressbar/styles/loadbar.css` with this to smoothly hide the floating loading bar when the URL bubble expands:

```css
/* Fix for the floating loadbar in compact mode */
@media (-moz-bool-pref: "zen.view.compact.hide-toolbar") {
  :root:not([zen-single-toolbar='true']):has([zen-compact-mode='true']) {
    &:has(#zen-appcontent-navbar-wrapper[zen-has-hover]),
    &:has(#zen-appcontent-navbar-wrapper[zen-user-show]),
    &:has(#zen-appcontent-navbar-wrapper[has-popup-menu]),
    &:has(*:is(#zen-appcontent-navbar-wrapper[panelopen='true'], 
               #zen-appcontent-navbar-wrapper[open='true'], 
               #urlbar:focus-within:not(#urlbar[zen-floating-urlbar='true']), 
               #zen-appcontent-navbar-wrapper[breakout-extend='true'])
          :not(.zen-compact-mode-ignore)
    ) {
      .browserSidebarContainer.deck-selected::before {
        opacity: 0 !important;
        top: 0px !important;
      }
    }
  }
}
```

</details>
