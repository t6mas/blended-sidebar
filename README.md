# Blended Sidebar

Applies the same page-aware adaptive color that **Blended Addressbar** uses on the URL bar to the left sidebar icon strip.

<p align="center">
  <img src="Captura.jpg" alt="Tema Azul Oscuro" width="45%" />
  <img src="Captura3.jpg" alt="Tema Verde Adaptado" width="45%" />
</p>

## Requirement

**Blended Addressbar must be installed and enabled.** This mod only adds CSS — it reuses the `--zen-tab-header-background` and `--zen-tab-header-foreground` variables that blended-addressbar's script writes on every tab change.

## Installation

1. Copy the `blended-sidebar` folder into `[Zen profile]/chrome/sine-mods/`.
2. Reload Sine or restart Zen Browser.
3. Enable **Blended Sidebar** from Sine settings.

## Files

- `theme.json` — Sine mod manifest
- `style.css` — applies the adaptive color variables to the sidebar
