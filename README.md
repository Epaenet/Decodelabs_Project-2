# Decodelabs_Project-2
# Responsive Layout — Project Submission

A simple, clean, fully responsive webpage built with **only HTML and CSS** — no JavaScript at all. It demonstrates the core fundamentals of responsive design: media queries, a collapsing navigation menu, and a flexible grid layout, all using pure CSS techniques.

---

## 1. File structure

```
basic-responsive-site/
├── index.html   → Markup and structure
└── style.css    → All styling, layout, and responsive rules
```

Just open `index.html` in any browser — no server, build step, or script files required.

---

## 2. Page sections

| Section | Purpose |
|---|---|
| **Header / Nav** | Sticky navigation bar with logo and links |
| **Hero** | Page introduction with a heading, subtext, and call-to-action button |
| **About** | A short paragraph describing the project |
| **Services** | A 3-card grid showcasing key features |
| **Contact** | A simple call-to-action with a mailto link |
| **Footer** | Copyright line |

---

## 3. How the mobile navigation works without JavaScript

This is the most important technique in the project, often called the **"checkbox hack."**

```html
<input type="checkbox" id="navCheck" class="nav-checkbox">
<nav>
  <ul class="nav-links">...</ul>
</nav>
<label for="navCheck" class="nav-toggle">
  <span></span><span></span><span></span>
</label>
```

**How it works step by step:**

1. A real `<input type="checkbox">` is placed in the markup but visually hidden with CSS (`opacity: 0`, `width: 0`, `height: 0`).
2. The hamburger icon is a `<label for="navCheck">` rather than a button. Clicking *any* `<label>` automatically toggles the checkbox it's linked to via its `for` attribute — this is standard HTML behavior, not a script.
3. CSS then reads the checkbox's `:checked` state using the **general sibling selector (`~`)**, which matches any sibling element that comes *after* the checkbox in the markup:

```css
.nav-checkbox:checked ~ .nav-links {
  transform: translateX(0);  /* or translateY(0) — slides menu into view */
  opacity: 1;
  visibility: visible;
}
```

4. The same trick animates the hamburger icon into an "X":

```css
.nav-checkbox:checked ~ .nav-toggle span:nth-child(1) { transform: rotate(45deg); }
.nav-checkbox:checked ~ .nav-toggle span:nth-child(2) { opacity: 0; }
.nav-checkbox:checked ~ .nav-toggle span:nth-child(3) { transform: rotate(-45deg); }
```

**Why this matters for the markup order:** the checkbox must appear *before* both the nav links and the label in the HTML, because the `~` selector only looks forward at later siblings, never backward.

---

## 4. Media queries

The layout adjusts at three breakpoints, applied from large screens down to small:

| Breakpoint | Screen type | Changes |
|---|---|---|
| `max-width: 1024px` | Tablets / small laptops | Card grid goes from 3 columns → 2 |
| `max-width: 768px` | Large phones / small tablets | Nav collapses into the checkbox-driven dropdown menu |
| `max-width: 480px` | Phones | Card grid goes to 1 column; section padding tightens |

---

## 5. Layout techniques used

- **Flexbox** — for the navigation bar (logo, links, and toggle laid out in a row with `justify-content: space-between`)
- **CSS Grid** — for the services card section (`grid-template-columns: repeat(3, 1fr)`, adjusted per breakpoint)
- **CSS custom properties (variables)** — all colors and spacing values (`--gap-sm`, `--gap-md`, `--gap-lg`, etc.) are defined once on `:root`, so spacing stays consistent everywhere and is easy to adjust globally
- **` clamp()`** — used on the hero heading so its font size scales smoothly between a minimum and maximum instead of jumping at breakpoints
- **A reusable `.container` class** — centers content and applies consistent side padding at every screen width

---

## 6. Why no JavaScript?

Removing JavaScript entirely forces every interactive behavior to be expressed as a CSS state — in this case, the checkbox's checked/unchecked state. This keeps the project:

- **Lightweight** — no script to download or parse
- **Resilient** — the menu still works even if JavaScript is disabled in the browser
- **A clear demonstration of CSS selectors** — particularly the general sibling selector (`~`) and the `:checked` pseudo-class, which are useful, real-world CSS skills beyond just toggling a menu

The trade-off: more complex interactive behavior (like animated counters or live data) genuinely does need JavaScript — the checkbox hack only works for simple two-state toggles like this menu.

---

## 7. Browser support

Uses only standard CSS features — Flexbox, Grid, custom properties, and basic pseudo-classes/selectors. Works in all current versions of Chrome, Firefox, Safari, and Edge, on desktop and mobile.
