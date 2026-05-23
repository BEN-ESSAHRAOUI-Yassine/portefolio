# 06 — Interactions & Animations

## General Principles

- **Performance first:** use `transform` and `opacity` for animations — never `width`, `height`, `top`, `left`.
- **Respect `prefers-reduced-motion`:** all animations must be disabled or reduced when this media query is active.
- **No animation libraries** — pure CSS transitions + JavaScript where needed.
- **Transition speed:** 200–300ms for UI feedback, 500–800ms for entrance animations.

---

## Page Load

- Fade-in + slight translateY(-10px → 0) on body content
- Hero text appears 200ms after load
- Staggered entrance for nav links (50ms delay each)

---

## Scroll Animations

Use `IntersectionObserver` to add `.visible` class when elements enter viewport.

```css
.animate-on-scroll {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.animate-on-scroll.visible {
  opacity: 1;
  transform: translateY(0);
}
```

**Elements that animate on scroll:**
- Section headers
- Skill badges (staggered, 30ms each)
- Timeline items (left-to-right slide)
- Project cards (staggered, 80ms each)
- Testimonial cards
- Stat badges (count-up animation on number)

---

## Hero Typewriter

```js
const roles = ["Full Stack Developer", "PHP & Laravel Engineer", "Automation Specialist"];
// Type forward at 80ms/char, pause 2000ms, delete at 40ms/char, pause 500ms, next
```

---

## Stat Counter (About section)

On scroll into view, numbers count up from 0 to target value over ~1.5s.
Use `requestAnimationFrame` with easeOut curve.

---

## Theme / Mode Transitions

```css
*, *::before, *::after {
  transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}
```

Applied globally so all elements smoothly transition when theme/mode changes.

---

## Navbar

- On scroll down past 60px: navbar gains `backdrop-filter: blur(12px)` + border-bottom
- On scroll up: navbar becomes more transparent
- Active nav link: underline slides to current section (CSS width transition)

---

## Project Cards

- Hover: `transform: translateY(-4px)`, deepened shadow
- `bold` theme: `box-shadow: 0 0 0 1px var(--color-accent), 0 8px 32px rgba(99,102,241,0.2)`
- Click ripple effect (optional)

---

## Skill Badges

- Hover: `transform: translateY(-2px) scale(1.03)`, accent border appears
- `bold` theme: subtle glow on hover

---

## Contact Form

- Input focus: border transitions to `var(--color-accent)`
- Submit button: loading spinner state while processing
- Error states: red border + shake animation on invalid submit
- Success: green checkmark fade-in

---

## Hamburger Menu (Mobile)

- 3-line → X icon transition (CSS transform)
- Menu slides down with `max-height` transition

---

## Scroll To Top Button

- Appears with fade-in after 300px scroll
- Disappears at top
- Click: smooth scroll to top

---

## Cursor (Bold theme only, desktop)

- Optional: custom cursor dot that follows mouse with slight lag (requestAnimationFrame)
- Only active on `data-theme="bold"` and non-touch devices

---

## `prefers-reduced-motion` Override

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
  .animate-on-scroll {
    opacity: 1;
    transform: none;
  }
}
```
