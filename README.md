# S.V. Mohammed Saqib — Premium Portfolio

A single-file, dark, instrumentation-inspired portfolio site with a draggable 3D hero node, scroll-triggered reveals, and animated skill bars. Built as one self-contained `portfolio.html` — no build step, no dependencies to install.

## Live preview

Just open `portfolio.html` in any modern browser (Chrome, Edge, Firefox, Safari). Everything — fonts, scripts, and both photos — loads either from CDN or is embedded directly in the file, so it works offline except for the Google Fonts and CDN script tags.

## Tech stack

| Layer | Tool | Loaded via |
|---|---|---|
| Structure & styling | HTML5, CSS3 (custom properties, no framework) | inline |
| Fonts | Space Grotesk, IBM Plex Sans, IBM Plex Mono | Google Fonts CDN |
| 3D hero visual | Three.js r128 | cdnjs |
| Scroll & entrance animation | GSAP 3 + ScrollTrigger | cdnjs |
| Photos | Embedded as base64 data URIs | inline (no external image files) |

No npm, no bundler, no build process — it's plain HTML/CSS/JS in one file.

## File structure

```
portfolio.html   ← everything: markup, styles, scripts, and images
```

That's the whole project. If you want to split it up later (e.g. for a React rebuild), the natural seams are:
- `<style>` block → CSS file / Tailwind config
- Hero 3D script → a `SensorNode` component
- ScrollTrigger reveals → a `useScrollReveal` hook
- Each `<section>` → its own component

## Sections

1. **Hero** — headline, CTA buttons, stats, and the draggable 3D node with your headshot at the center
2. **About** — bio + outdoor photo + quick-facts list (location, focus, education, stack)
3. **Work** — Krishi Setu, eActuell, CineQuest, each with stack tags and role/duration
4. **Skills** — three columns (Frontend / Backend & data / Foundations) with animated proficiency bars
5. **Experience** — simple timeline (Krishi Setu → eActuell → education)
6. **Contact** — email + link placeholders, footer

## Customizing content

Everything is plain text/HTML inside `portfolio.html` — search for these anchors:

- **Contact info**: search for `your.email@example.com` and the `contact-links` block (GitHub / LinkedIn / Resume `href="#"` placeholders) — replace with your real links
- **Hero stats**: `hero-stats` block — the three `<div class="hero-stat">` entries
- **Projects**: each `<div class="project">` block under `<!-- WORK -->`
- **Skill bar levels**: each `.bar-fill` has a `data-w="NN"` attribute (0–100) controlling fill width
- **Timeline entries**: `<div class="tl-item">` blocks under `<!-- EXPERIENCE TIMELINE -->`

## Customizing design

All colors, fonts, and spacing tokens live at the top of the `<style>` block under `:root`:

```css
--bg:#0A0E13;        /* page background */
--bg-alt:#10161D;     /* panel surface */
--line:#223140;       /* hairline borders */
--text:#E9EDEF;       /* primary text */
--text-dim:#8FA0AC;   /* secondary text */
--accent:#F2A93B;     /* amber signal accent */
--accent-2:#4FD1C5;   /* teal secondary accent */
```

Change these and the whole site re-themes — no other edits needed.

## Replacing the photos

Both photos are embedded as base64 so the file stays portable. To swap them:
1. Convert your new image to a data URI (e.g. `base64 -i yourphoto.jpg` on Mac/Linux, or any online base64 encoder)
2. Replace the string inside `src="data:image/jpeg;base64,..."` for:
   - `.hero-photo img` (the circular headshot in the hero)
   - `.about-photo img` (the photo in the About section)

Alternatively, replace the `src` with a normal image path (e.g. `images/headshot.jpg`) if you'd rather keep photos as separate files — just make sure that file ships alongside `portfolio.html` if you do.

## Deploying

Since it's a single static HTML file, it runs on any static host:

- **GitHub Pages**: push to a repo, rename to `index.html`, enable Pages
- **Vercel / Netlify**: drag-and-drop deploy, or connect the repo
- **Any web host**: upload `portfolio.html` (renamed to `index.html`) via FTP

No environment variables, no server, no build command required.

## Accessibility & performance notes

- Respects `prefers-reduced-motion` — animations are disabled for users who request it
- All interactive elements have visible focus states
- Images are pre-compressed (~50–90 KB each) before embedding to keep page weight reasonable
- The 3D canvas and GSAP scripts are the only things blocking full "no-JS" rendering — content is still readable with JS disabled, just without motion

## Credits

- [Three.js](https://threejs.org/) — 3D rendering
- [GSAP](https://gsap.com/) + [ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/) — animation
- [Google Fonts](https://fonts.google.com/): Space Grotesk, IBM Plex Sans, IBM Plex Mono
