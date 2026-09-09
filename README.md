# Animated gradient border on a transparent background

A small static CSS/HTML demo of a glassmorphism panel with a **rotating conic-gradient border** that stays transparent in the middle (so a video or page background shows through).

This is not an npm package and not a framework component library. It is a self-contained demo: `index.html` + `style.css`.

## What it does

- `.border-gradient` draws a border via an `::after` layer with a `conic-gradient`, then punches out the interior with CSS masks:
  - `mask-composite: exclude`
  - `-webkit-mask-composite: xor`
- `.border-glow` adds a blurred glow layer (`::before`) using the same angle.
- `.animate-rotate-angle` spins both layers with `@property --conic-gradient-angle` and a `@keyframes background-spin` animation (3s linear infinite).
- `.glass` is a translucent panel (gradients + inset shadows).
- Dark/light toggle via a checkbox (`.darklight`) and `prefers-color-scheme`.
- Custom CSS `@function` helpers (`--transparency`, `--light-dark`) live in `style.css` — browser support for CSS `@function` is limited; treat that as experimental.

## Run locally

No build step. Serve the folder over HTTP (needed if the remote video background is blocked by mixed-content or CORS quirks when opening as `file://`):

```bash
# Python
python3 -m http.server 8080

# or any static server pointed at this directory
```

Then open `http://localhost:8080/`.

Or open `index.html` directly in a Chromium-based browser for a quick look.

## Use the classes elsewhere

Copy the relevant rules from `style.css` (especially `.border-gradient`, `.border-glow`, `.animate-rotate-angle`, and the `@property` / `@keyframes` block). Example markup from the demo:

```html
<div class="glass rounded border-gradient border-glow animate-rotate-angle m p shadow">
  <h2>What is it?</h2>
  <p>Glass panel with a rotating gradient border, transparent in the middle via masks.</p>
</div>
```

Tune CSS variables on `.border-gradient` / `.border-glow` such as `--border-width`, `--border-radius`, `--glow-spread`, `--glow-blur`, and `--gradient-colors`.

## Files

| File | Role |
|------|------|
| `index.html` | Demo page |
| `style.css` | All styles and the mask/animation technique |
| `bg.png`, `video.webm`, screenshots | Demo assets |
| `LICENSE.md` | GPL-3.0 |

## Requirements

Modern browser with support for:

- CSS `@property` (typed custom properties)
- `mask` / `-webkit-mask` + `mask-composite` / `-webkit-mask-composite`
- `conic-gradient`
- Optionally CSS `@function` (used for helpers; may need fallbacks in production)

## License

GPL-3.0 — see `LICENSE.md`.
