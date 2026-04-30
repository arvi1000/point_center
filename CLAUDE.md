# point center — coding agent notes

## What this is
A single-file static web utility (`index.html`) that lets users click on a Leaflet map to place points and see the geographic centroid update in real time. No build step, no npm, no server required.

## Stack
- **Leaflet 1.9.4** via CDN — map tiles from OpenStreetMap
- Plain HTML/CSS/JS — no framework, no bundler
- Everything lives in `index.html`

## Key design decisions
- Centroid is arithmetic mean of all point latitudes and longitudes. This is a flat-earth approximation; it is accurate enough for points that aren't widely spread across the globe, and is the simplest correct algorithm.
- Dashed lines from each point to the centroid are purely visual feedback — they re-render on every update via remove/re-add.
- The centroid marker uses a `divIcon` with CSS class `centroid-marker` (pink dot + glow ring). Point markers use `point-marker` (blue dot). Both are styled in `<style>`.

## File layout
```
index.html   — entire app (map, logic, styles)
README.md    — user-facing docs
CLAUDE.md    — this file
```

## Common tasks

### Adding a feature
Edit `index.html` directly. Keep all JS in the `<script>` block at the bottom. Keep all styles in the `<style>` block in `<head>`.

### Testing locally
Open `index.html` in a browser. No server needed — all external resources load from CDN.

### Changing the centroid calculation
The `centroid()` function at the top of the script block is the only place the math lives.

### Changing colors / appearance
All visual styling is in the `<style>` block. The color palette follows Catppuccin Mocha:
- Background: `#1e1e2e`
- Text: `#cdd6f4`
- Point color (blue): `#89b4fa`
- Centroid color (pink): `#f38ba8`
- Accent (purple): `#cba6f7`

## Things to avoid
- Don't add a build step or npm dependency — the point of this project is zero-friction setup.
- Don't use a map provider that requires an API key; stick with OpenStreetMap tiles.
- Don't split into multiple files unless the single file meaningfully exceeds ~300 lines.
