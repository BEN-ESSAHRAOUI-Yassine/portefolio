# 02 — Theming System

## Overview

Two independent systems working together:

1. **Profile switcher** — 3 professional profiles (tabs in navbar), each with unique content + color palette
2. **Dark / Light mode** — separate toggle, works across all profiles

Combined: 6 visual variants. Both persisted in `localStorage`, applied as attributes on `<html>`:

```html
<html data-profile="dev" data-mode="dark">
```

---

## Profile Switcher (Navbar Tabs)

Three visible tab buttons in the navbar:

```
[ 💻 Dev ]  [ 📡 Telecom ]  [ 🔧 IT Support ]       [ ☀ Mode ]
```

- Active tab: filled/highlighted with profile accent color
- Inactive tabs: muted, outline style
- Switching profile: changes accent color palette + visible content sections simultaneously
- Smooth transition: 0.3s on colors, content swap is instant (show/hide via CSS classes or JS)

---

## Dark / Light Toggle

- Sun/Moon icon button, far right of navbar
- Toggles `data-mode="dark"` ↔ `data-mode="light"`
- Default: `dark`

---

## Profile 1: Dev — Full Stack Developer
**Accent:** Blue / Indigo
**Style vibe:** Minimal & clean — Linear, Vercel aesthetic

| Token | Light | Dark |
|-------|-------|------|
| `--bg-primary` | `#ffffff` | `#0a0a0a` |
| `--bg-secondary` | `#f5f5f5` | `#111111` |
| `--bg-card` | `#fafafa` | `#1a1a1a` |
| `--text-primary` | `#0a0a0a` | `#f0f0f0` |
| `--text-secondary` | `#555555` | `#888888` |
| `--color-accent` | `#4f46e5` | `#6366f1` |
| `--color-accent-hover` | `#4338ca` | `#818cf8` |
| `--border` | `#e5e5e5` | `#222222` |
| `--radius` | `8px` | `8px` |

---

## Profile 2: Telecom — FTTH / GIS Engineer
**Accent:** Teal / Cyan
**Style vibe:** Bold & technical — maps, infrastructure, precision

| Token | Light | Dark |
|-------|-------|------|
| `--bg-primary` | `#f0fdfc` | `#020f0f` |
| `--bg-secondary` | `#e0f7f5` | `#071a1a` |
| `--bg-card` | `#ffffff` | `#0d2424` |
| `--text-primary` | `#0d2424` | `#e0fdfc` |
| `--text-secondary` | `#3d7a75` | `#5eaaaa` |
| `--color-accent` | `#0d9488` | `#2dd4bf` |
| `--color-accent-hover` | `#0f766e` | `#5eead4` |
| `--border` | `#b2dfdb` | `#133a3a` |
| `--radius` | `6px` | `6px` |

---

## Profile 3: IT Support — Maintenance & Networks
**Accent:** Orange / Amber
**Style vibe:** Professional & corporate — structured, clear hierarchy

| Token | Light | Dark |
|-------|-------|------|
| `--bg-primary` | `#fffbf5` | `#100a00` |
| `--bg-secondary` | `#fff3e0` | `#1a1000` |
| `--bg-card` | `#ffffff` | `#221500` |
| `--text-primary` | `#1a0f00` | `#fff3e0` |
| `--text-secondary` | `#7a5c2e` | `#b08040` |
| `--color-accent` | `#ea580c` | `#fb923c` |
| `--color-accent-hover` | `#c2410c` | `#fdba74` |
| `--border` | `#fed7aa` | `#2e1a00` |
| `--radius` | `4px` | `4px` |

---

## CSS Implementation Pattern

```css
/* Each profile+mode combination sets all tokens */
[data-profile="dev"][data-mode="dark"] {
  --bg-primary: #0a0a0a;
  --color-accent: #6366f1;
  /* ... */
}
[data-profile="dev"][data-mode="light"] {
  --bg-primary: #ffffff;
  --color-accent: #4f46e5;
  /* ... */
}
[data-profile="telecom"][data-mode="dark"] { /* teal dark tokens */ }
[data-profile="telecom"][data-mode="light"] { /* teal light tokens */ }
[data-profile="it"][data-mode="dark"] { /* orange dark tokens */ }
[data-profile="it"][data-mode="light"] { /* orange light tokens */ }

/* All components use variables only */
.card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius);
}
```

---

## Content Visibility per Profile

Sections are shown/hidden using profile data attributes:

```html
<!-- Only visible in dev profile -->
<section class="profile-section" data-show-in="dev">...</section>

<!-- Only visible in telecom profile -->
<section class="profile-section" data-show-in="telecom">...</section>

<!-- Visible in all profiles -->
<section class="profile-section" data-show-in="all">...</section>
```

```css
.profile-section { display: none; }
.profile-section[data-show-in="all"] { display: block; }

[data-profile="dev"] .profile-section[data-show-in="dev"] { display: block; }
[data-profile="telecom"] .profile-section[data-show-in="telecom"] { display: block; }
[data-profile="it"] .profile-section[data-show-in="it"] { display: block; }
```

---

## JS Logic

```js
const profiles = ['dev', 'telecom', 'it'];

function setProfile(name) {
  document.documentElement.setAttribute('data-profile', name);
  localStorage.setItem('profile', name);
  // Update active tab UI
  document.querySelectorAll('.profile-tab').forEach(tab => {
    tab.classList.toggle('active', tab.dataset.profile === name);
  });
}

function toggleMode() {
  const current = document.documentElement.getAttribute('data-mode');
  const next = current === 'dark' ? 'light' : 'dark';
  document.documentElement.setAttribute('data-mode', next);
  localStorage.setItem('mode', next);
}

// On load: restore preferences
const savedProfile = localStorage.getItem('profile') || 'dev';
const savedMode = localStorage.getItem('mode') || 'dark';
document.documentElement.setAttribute('data-profile', savedProfile);
document.documentElement.setAttribute('data-mode', savedMode);
```
