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

1. Download the zip file from "code"
2. Open your Zen Browser profile folder (e.g., `C:\Users\YourUser\AppData\Roaming\zen\Profiles\[your-profile]\chrome\sine-mods\`).
3. Copy the `blended-sidebar` folder into the `sine-mods` directory.
4. Open the `mods.json` file located in the `sine-mods` folder.
5. Carefully paste the following configuration inside the main object (don't forget to add a comma before it if it's not the first item):

```json
,"blended-sidebar":{"id":"blended-sidebar","name":"Blended Sidebar","description":"A sidebar that adapts to the page and combines the Zen Chrome aesthetic with the active website.","author":"based on blended-addressbar by kkugot","version":"1.0.0","updatedAt":"2026-05-09","tags":["sidebar","adaptive","theming","zen browser"],"fork":["zen"],"scripts":{"blended-sidebar.uc.js":{"include":["chrome://browser/content/browser.xhtml"]}},"style":{"chrome":"style.css","content":""},"readme":"README.md","js":true,"createdAt":"2026-05-09","no-updates":true,"enabled":true}
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

Replace the code in your original `blended-addressbar/style.css` file with this to restore vertical padding without altering the horizontal layout, and also remove the rounded design.

```css
@import "styles/loadbar.css";

:root {
    --blended-addressbar-frame-gap: 5px;
    --blended-addressbar-frame-radius: 14px;
    --blended-addressbar-frame-shadow:
        0 10px 24px rgba(0, 0, 0, 0.10),
        0 1px 4px rgba(0, 0, 0, 0.10);
}

@media (prefers-color-scheme: dark) {
    :root {
        --blended-addressbar-frame-shadow:
            0 12px 28px rgba(0, 0, 0, 0.30),
            0 1px 5px rgba(0, 0, 0, 0.28);
    }
}

/* URL bar */

/* Only in single toolbar mode */
:root:not([zen-single-toolbar="true"]) {

    /* Wrapper */

    #zen-appcontent-wrapper {
        z-index: 3;
        margin: var(--blended-addressbar-frame-gap) var(--blended-addressbar-frame-gap) var(--blended-addressbar-frame-gap) 0 !important;
        box-shadow: var(--blended-addressbar-frame-shadow);
        border-radius: var(--blended-addressbar-frame-radius);
        overflow: hidden;
        isolation: isolate;
        
    }

    @media -moz-pref("zen.tabs.vertical.right-side") {
        #zen-appcontent-wrapper {
            margin: var(--blended-addressbar-frame-gap) 0 var(--blended-addressbar-frame-gap) var(--blended-addressbar-frame-gap) !important;
        }
    }

    &:has([zen-compact-mode="true"]) {
        #zen-appcontent-wrapper {
            margin: var(--blended-addressbar-frame-gap) !important;
        }
    }

    &[chromehidden~="toolbar"],
    &:has(#navigator-toolbox[tabs-hidden]) {
        #zen-appcontent-wrapper {
            margin: 0 !important;
            border-radius: 0 0 var(--blended-addressbar-frame-radius) var(--blended-addressbar-frame-radius) !important;
        }
    }
    
    #tabbrowser-tabpanels,
    #tabbrowser-tabbox {
        overflow: hidden;
    }
    /* The URL bar with bookmarks */
    #zen-appcontent-navbar-wrapper {
        background-color: var(--zen-tab-header-background, var(--zen-main-browser-background-toolbar));
        box-shadow: none;
        color: var(--zen-tab-header-foreground, inherit);
        fill: currentColor;
        --toolbox-textcolor: currentColor;
        --toolbarbutton-icon-fill: currentColor;
        --toolbar-color: currentColor;
        --toolbar-field-color: currentColor;

        transition: background-color 100ms linear;

        #nav-bar-customization-target,
        #PersonalToolbar,
        #PanelUI-button {
            -moz-window-dragging: drag;
            color: var(--zen-tab-header-foreground, inherit);
            fill: currentColor;
            --toolbox-textcolor: currentColor;
            --toolbarbutton-icon-fill: currentColor;
            --toolbar-color: currentColor;
            --toolbar-field-color: currentColor;
            
        }
    }

    &:has([zen-compact-mode="true"]) #zen-appcontent-navbar-wrapper {
        :is(toolbarbutton, .toolbarbutton-1, .toolbarbutton-icon, .urlbar-icon) {
            color: inherit !important;
            fill: currentColor !important;
            --toolbarbutton-icon-fill: currentColor;
        }
    }

    #nav-bar {
        margin-inline-end: 0 !important;
        padding-inline-start: var(--zen-element-separation) !important;
        padding-inline-end: var(--zen-element-separation) !important;
    }
    #nav-bar,
    #PersonalToolbar {
        box-shadow: 0 -1px 0 0 inset rgba(128,128,128, 0.09);
    }

    /* The webpage content wrapper */
    #zen-tabbox-wrapper {
        margin: 0 !important;
        
    }
    
    /* Hide shadow and border - they are now in a parent element */
    #tabbrowser-tabbox #tabbrowser-tabpanels .browserSidebarContainer {
        :root:not([zen-no-padding="true"]) &:not(.zen-glance-overlay) {
            --zen-native-inner-radius: 0 0 var(--zen-native-inner-radius) var(--zen-native-inner-radius);
            --zen-big-shadow: none;
        }
    }
    
    /* Glance  modification*/
    .browserSidebarContainer.zen-glance-background.deck-selected {
         transform: scale(1) !important;
    }

    .zen-glance-overlay .browserContainer {
         height: 98% !important;
    }
    .urlbar-background {
        --zen-toolbar-element-bg: transparent;
    }

    /* Sidebar */
    #sidebar-box {
        border-radius: 0 !important;
    }
}

:root {
  --blended-addressbar-frame-gap: 0px;
  --blended-addressbar-frame-radius: 0px;
  --blended-addressbar-frame-shadow: none;
}

:root:not([zen-single-toolbar="true"]) {
  #zen-appcontent-wrapper {
    margin: 0 !important;
    box-shadow: none !important;
    border-radius: 0 !important;
    overflow: visible !important;
  }

  #zen-appcontent-navbar-wrapper {
    box-shadow: none !important;
  }

  .urlbar-background {
    --zen-toolbar-element-bg: unset;
  }
}

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

Replace in your original `blended-addressbar/styles/loadbar.css` with this to smoothly hide the floating loading bar when the URL bubble expands:

```css
@-moz-document url-prefix("chrome:") {
  .browserSidebarContainer.deck-selected::before {
    content: "" !important;
    position: absolute !important;
    top: 0px !important; 
    left: 0px !important;
    height: var(--blended-addressbar-loadbar-height, 2px) !important;
    max-width: 100% !important;
    width: var(--bar-pcent) !important;
    background-color: var(--bar-colour, var(--blended-addressbar-loadbar-color, var(--zen-primary-color))) !important; 
    opacity: var(--blended-addressbar-loadbar-opacity, 0.85) !important;
    
    @media (-moz-bool-pref: "uc.loadbar.shadow") {
      filter: drop-shadow(0px 0px 10px black) !important;
    }
    
    border-radius: 0 var(--blended-addressbar-loadbar-height, 2px) var(--blended-addressbar-loadbar-height, 2px) 0 !important;
    
    @media not (-moz-bool-pref: "uc.loadbar.roundedcorner") {
       border-radius: 0 !important;
    }
    
    z-index: 1 !important;
    transition: width 0.5s ease-in-out, top 0.1s ease-in-out, opacity 0.2s ease-in-out, background 0.2s ease !important;
  }

  @media not (-moz-bool-pref: "zen.view.compact.hide-toolbar") and not (-moz-bool-pref: "zen.view.use-single-toolbar") {
    .browserSidebarContainer.deck-selected::before {
      top: 39px !important; 
    }
  }
  
  .browserSidebarContainer.deck-selected:has([zen-glance-selected])::before,
  .browserSidebarContainer.deck-selected.zen-glance-overlay::before {
    max-width: calc(85%) !important;
    left: calc(15%/2) !important;
    border-radius: 6px !important;
  }
  
  .browserSidebarContainer.deck-selected.zen-glance-background::before {
    background: transparent !important;
    height: 0px !important;
  }
  
  :root {
    &:has(.tabbrowser-tab[selected][busy]) {
      --bar-colour: var(--blended-addressbar-loadbar-color, var(--zen-primary-color));
      --bar-pcent: 15%;
    }
    &:has(.tabbrowser-tab[selected][busy][pendingicon]) {
      --bar-colour: var(--blended-addressbar-loadbar-color, var(--zen-primary-color));
      --bar-pcent: 45%;
    }
    &:has(.tabbrowser-tab[selected][busy][pendingicon][progress]) {
      --bar-colour: var(--blended-addressbar-loadbar-color, var(--zen-primary-color));
      --bar-pcent: 85%;
    }
    &:has(.tabbrowser-tab[selected][busy][progress]) {
      --bar-colour: var(--blended-addressbar-loadbar-color, var(--zen-primary-color));
      --bar-pcent: 95%;
    }
    &:has(.tabbrowser-tab[selected][muted]:not([busy])) {
      --bar-colour: orangered;
      --bar-pcent: 100%;
      
      .browserSidebarContainer.deck-selected::before {
        border-radius: 0;
      }
    }
  }

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
}
```

</details>
