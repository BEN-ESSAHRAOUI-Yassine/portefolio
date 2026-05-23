# Agent Prompt — Portfolio Build

You are an expert frontend developer. Your task is to build a complete, production-quality personal portfolio website for Yassine BEN ESSAHRAOUI.

## Step 1 — Read the specs before writing any code

Read every file in the `specs/` folder in this order:

1. `specs/01-architecture.md` — output format, file structure, fonts, breakpoints
2. `specs/02-theming.md` — profile system, color tokens, CSS patterns, JS logic
3. `specs/03-sections.md` — all sections, per-profile content variants
4. `specs/04-content.md` — all real copy and data, `[PLACEHOLDER]` markers
5. `specs/05-components.md` — every UI component with HTML structure
6. `specs/06-interactions.md` — animations, scroll effects, transitions

Do not skip any file. Do not start coding until you have read all 6.

---

## Step 2 — What you are building

A **single `portfolio.html` file** — all CSS and JS embedded inline. No build step, no framework, no bundler. Pure HTML/CSS/JS with Google Fonts and Lucide icons via CDN.

### Core feature: 3-profile system + dark/light mode

The portfolio has **3 professional profiles** switchable from the navbar:

| Profile | Label | Accent Color | Vibe |
|---------|-------|-------------|------|
| `dev` | 💻 Dev | Blue / Indigo | Minimal, clean |
| `telecom` | 📡 Telecom | Teal / Cyan | Bold, technical |
| `it` | 🔧 IT Support | Orange / Amber | Corporate, structured |

Plus a **dark/light mode toggle** independent of the profile — 6 total variants.

Both are controlled via `data-profile` and `data-mode` attributes on `<html>`, persisted in `localStorage`.

When the user switches profile:
- The color palette changes instantly (CSS custom properties)
- The visible content changes (different hero text, skills, experience entries, projects)
- The typewriter animation resets to the new profile's roles

---

## Step 3 — Non-negotiable rules

1. **Never hardcode colors.** Every color must use a CSS custom property (`var(--color-accent)`, `var(--bg-card)`, etc.).
2. **All 6 CSS token sets must be defined** — one per `[data-profile][data-mode]` combination. See `specs/02-theming.md` for the exact values.
3. **Content visibility** is controlled with `data-show-in` attributes and CSS attribute selectors. See `specs/05-components.md` for the pattern.
4. **Mobile-first.** Base styles are for 375px. Use `min-width` media queries for tablet (768px) and desktop (1280px).
5. **No content invention.** Use only data from `specs/04-content.md`. Where `[PLACEHOLDER]` appears, render a clearly marked placeholder (e.g. `href="#"`, greyed-out text, or an empty avatar circle).
6. **Semantic HTML.** Use `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` appropriately. Add `aria-label` to all interactive elements.
7. **Profile tabs stay visible on mobile** — do not hide them in the hamburger menu.
8. **Smooth profile/mode transitions** — apply `transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease` globally.
9. **Respect `prefers-reduced-motion`** — wrap all animations in a media query check. See `specs/06-interactions.md`.
10. **Output is one file:** `portfolio.html`. Do not split into multiple files.

---

## Step 4 — Section order and structure

Build sections in this order inside `<main>`:

```
#hero → #about → #skills → #experience → #projects → #testimonials → #contact
```

Each section must have the `animate-on-scroll` class and become visible via `IntersectionObserver`.

Refer to `specs/03-sections.md` for the exact content per profile per section.

---

## Step 5 — Fonts and icons

```html
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

<!-- Lucide Icons -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
```

Use `Space Grotesk` for headings, `Inter` for body, `JetBrains Mono` for skill badges and code-style labels.

After the closing `</body>` call `lucide.createIcons()` to render icons.

---

## Step 6 — JS requirements

Implement these functions in a single `<script>` block at the bottom of `<body>`:

```js
// Profile switching
function setProfile(name) { ... }

// Dark/light toggle
function toggleMode() { ... }

// Typewriter — resets on profile switch, uses per-profile role arrays
function initTypewriter() { ... }

// IntersectionObserver for scroll animations
function initScrollAnimations() { ... }

// Stat counter (count up from 0 on scroll into view)
function initStatCounters() { ... }

// Navbar scroll behavior (blur + border on scroll)
function initNavbar() { ... }

// Scroll-to-top button
function initScrollToTop() { ... }

// Hamburger menu toggle
function initHamburger() { ... }

// On load: restore localStorage preferences, then init all
```

---

## Step 7 — Quality checklist before finishing

Before outputting the final file, verify:

- [ ] All 6 color token sets are defined (3 profiles × 2 modes)
- [ ] Switching profile changes both color AND content simultaneously
- [ ] Dark/light toggle works independently in all 3 profiles
- [ ] Typewriter shows the correct roles for the active profile
- [ ] `data-show-in` filtering works for: hero variants, about bio, skill groups, timeline items, project cards
- [ ] All sections animate on scroll
- [ ] Stat counters count up on scroll into view
- [ ] Navbar is sticky, blurs on scroll, active link tracks scroll position
- [ ] Mobile hamburger works, profile tabs always visible
- [ ] Contact form validates client-side and uses mailto fallback
- [ ] Scroll-to-top button appears after 300px
- [ ] `[PLACEHOLDER]` items are rendered gracefully (not broken)
- [ ] `prefers-reduced-motion` disables animations
- [ ] No hardcoded color values anywhere in CSS

---

## Output

Produce a single file: `portfolio.html`

It must open correctly in any modern browser with no server required (just `open portfolio.html` or drag into browser).
