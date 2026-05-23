# 05 — Components

All reusable UI components. CSS custom properties only — no hardcoded colors.

---

## Navbar

```
[ Yassine BEN ESSAHRAOUI ]   [ 💻 Dev | 📡 Telecom | 🔧 IT ]   [ About Skills Projects Contact ]   [ ☀ ]
```

- Sticky top, `backdrop-filter: blur(12px)` + semi-transparent bg
- **Profile tabs:** 3 pill buttons, active one filled with `var(--color-accent)`
- **Mode toggle:** sun/moon icon, far right
- Active nav link tracks scroll via IntersectionObserver
- Mobile: hamburger → slide-down menu (profile tabs stay visible)

---

## ProfileTabs

```html
<div class="profile-tabs">
  <button class="profile-tab active" data-profile="dev">💻 Dev</button>
  <button class="profile-tab" data-profile="telecom">📡 Telecom</button>
  <button class="profile-tab" data-profile="it">🔧 IT</button>
</div>
```

- Active tab: `background: var(--color-accent)`, white text
- Inactive tabs: transparent bg, `var(--text-secondary)` color, border `var(--border)`
- On click: calls `setProfile(name)` → updates `data-profile` on `<html>` → CSS handles content visibility + color tokens instantly
- Transition: 0.3s color, bg

---

## ModeToggle

- Icon only (☀ / 🌙)
- Tooltip: "Light mode" / "Dark mode"
- On click: calls `toggleMode()`

---

## HeroTypewriter

- Cycles through role strings per active profile
- Profiles each have their own array of roles (see specs/03-sections.md)
- Speed: 80ms/char type, 40ms/char delete, 2000ms pause
- Profile switch resets typewriter to new profile's roles immediately

---

## SkillBadge

```html
<span class="skill-badge">
  <span class="skill-icon">⚙️</span>
  <span class="skill-label">Laravel</span>
</span>
```

Hover: accent border + `translateY(-2px)`

---

## SkillGroup

```html
<div class="skill-group" data-show-in="dev">
  <h3 class="skill-group-title">Backend</h3>
  <div class="skill-badges"><!-- badges --></div>
</div>
```

`data-show-in` controls which profile shows this group.

---

## TimelineItem

```html
<div class="timeline-item" data-show-in="dev telecom">
  <div class="timeline-dot"></div>
  <div class="timeline-content">
    <h3>Job Title</h3>
    <span class="timeline-company">Company</span>
    <span class="timeline-date">2022 – 2024</span>
    <ul>...</ul>
  </div>
</div>
```

Note: `data-show-in` can contain multiple space-separated profile names.

```css
.timeline-item { display: none; }
[data-profile="dev"] .timeline-item[data-show-in*="dev"] { display: flex; }
[data-profile="telecom"] .timeline-item[data-show-in*="telecom"] { display: flex; }
[data-profile="it"] .timeline-item[data-show-in*="it"] { display: flex; }
```

---

## ProjectCard

```html
<div class="project-card" data-show-in="dev">
  <div class="project-header">
    <h3>GameCafé Manager</h3>
    <div class="project-links">
      <a href="#">GitHub</a>
      <a href="#">Demo</a>
    </div>
  </div>
  <p>Description...</p>
  <div class="project-tags">
    <span class="tag">PHP</span>
    <span class="tag">MySQL</span>
  </div>
</div>
```

Hover: `translateY(-4px)`, deeper shadow, accent border glow.

---

## AboutBio

```html
<p class="about-bio" data-show-in="dev">Dev bio text...</p>
<p class="about-bio" data-show-in="telecom">Telecom bio text...</p>
<p class="about-bio" data-show-in="it">IT bio text...</p>
```

Only one visible at a time.

---

## StatBadge

```html
<div class="stat-badge">
  <span class="stat-number" data-target="7">0</span>
  <span class="stat-suffix">+</span>
  <span class="stat-label">Années d'exp.</span>
</div>
```

Count-up animation on scroll into view.

---

## TestimonialCard

```html
<div class="testimonial-card">
  <p class="quote">"..."</p>
  <div class="testimonial-author">
    <div class="author-avatar">AB</div>
    <div>
      <strong>Name</strong>
      <span>Role — Company</span>
    </div>
  </div>
</div>
```

---

## ContactForm

Fields: Name, Email, Subject, Message, Submit.
Client-side validation + mailto fallback. Shared across all profiles.

---

## SectionHeader

```html
<div class="section-header">
  <h2>Section Title</h2>
  <p class="section-subtitle">Subtitle</p>
  <div class="section-divider"></div>
</div>
```

`section-divider`: 48px wide, 3px tall, `var(--color-accent)` — changes color with profile.

---

## ScrollToTopButton

Fixed bottom-right. Appears after 300px scroll. Smooth scroll to top.
