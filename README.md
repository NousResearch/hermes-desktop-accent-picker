> [!IMPORTANT]
> **This repo has moved.** The plugin now lives in [`NousResearch/hermes-official-plugins/accent-picker`](https://github.com/NousResearch/hermes-official-plugins/tree/main/accent-picker), the single repo for Nous's official Hermes plugins. Its history, open issues and pull requests went with it, and this repo is archived.
>
> Already installed? `hermes plugins update` moves you to the new home automatically. New install: `hermes plugins install` from the plugin catalog.

# Accent Picker — Hermes Desktop plugin

An OKLCH colour wheel in the Hermes Desktop status bar. Drag it and the whole
theme retints live; the palette re-derives from the one colour you pick. It is
an **authoring tool** for theme designers — the colour is scratch state and is
never persisted. Two palette commands come with it: *Accent: reset to the theme
default* and *Accent: copy the current color*.

It used to ship bundled with the app (off by default). It now lives here as a
standalone desktop plugin so the app's plugin list only carries things most
users want.

## Install

Hermes Desktop → **Capabilities → Plugins → Install from Git**, paste

```
https://github.com/NousResearch/hermes-desktop-accent-picker
```

and tick the *Desktop UI* half. Or by hand:

```bash
git clone https://github.com/NousResearch/hermes-desktop-accent-picker \
  ~/.hermes/desktop-plugins/accent
```

The app watches `~/.hermes/desktop-plugins/` and loads `plugin.js` within a few
seconds; flip the switch in Capabilities → Plugins to enable it.

## Layout

- `plugin.js` — the loadable artifact. Plain ESM, only imports
  `@hermes/plugin-sdk`, `react`, and `react/jsx-runtime` (the three specifiers
  the desktop plugin loader resolves).
- `src/plugin.tsx`, `src/picker.tsx` — the TSX source it is built from.

## Build

```bash
npm install
npm run build   # esbuild src/plugin.tsx → plugin.js
```

Commit the rebuilt `plugin.js`; the desktop loads files uncompiled, so the
artifact is what ships.

## SDK

Everything the picker uses comes from `@hermes/plugin-sdk`: `$accentOverride`,
`setAccentOverride`, the OKLCH helpers (`hexToOklch`, `oklchToHex`,
`oklchToSrgb255`, `maxChroma`, `contrastRatio`), `Popover*`, `useTheme`,
`useValue`, `STATUSBAR_AREAS`, `PALETTE_AREA`. Reference:
https://hermes-agent.nousresearch.com/docs/developer-guide/desktop-plugin-sdk

MIT.
