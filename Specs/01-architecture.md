# 01 — Architecture

## Output Format

**Single HTML file** — all CSS and JS embedded inline.
Optionally exportable as a React `.jsx` artifact for Claude rendering.

## File Structure (single-file approach)

```
portfolio.html
├── <head>
│   ├── Meta, title, fonts (Google Fonts via CDN)
│   └── <style> — all CSS including theme variables
├── <body data-theme="minimal" data-mode="dark">
│   ├── #navbar — sticky top nav + theme/mode switchers
│   ├── #hero
│   ├── #about
│   ├── #skills
│   ├── #experience
│   ├── #projects
│   ├── #testimonials
│   └── #contact
└── <script> — all JS (theme toggle, scroll, animations)
```

## Fonts

- **Headings:** `Inter` or `Space Grotesk` (Google Fonts)
- **Body:** `Inter`
- **Code/tech labels:** `JetBrains Mono`

## Responsive Breakpoints

| Name | Width |
|------|-------|
| Mobile | 375px+ |
| Tablet | 768px+ |
| Desktop | 1280px+ |

## Navigation

- Sticky top navbar
- Logo/name left, nav links center/right
- On mobile: hamburger menu
- Active section highlighted via IntersectionObserver
- Smooth scroll to sections on click

## No build step required

Pure HTML/CSS/JS. No bundler, no framework dependency. CDN only for fonts and icons (e.g. Lucide or Heroicons via CDN).
