# Page Background Wave Decoration — Design Spec

**Date**: 2026-08-11
**Status**: Approved
**Scope**: Add a fixed bottom wave decoration to the page background

---

## 1. Purpose

The homepage background is currently plain white (`$background-color: #fff`), which feels monotonous. Add a subtle, math-themed decorative wave at the bottom of the page — echoing the "computational mathematics / PDE" identity of the site — without distracting from content readability.

---

## 2. Visual Design (user-approved via visual companion)

| Aspect | Decision |
|--------|----------|
| Style | Two stacked, softly-colored sine-wave layers (SVG bezier curves) |
| Position | `position: fixed` at the bottom of the viewport, full width — always visible while scrolling |
| Color | Based on template primary `$info-color: #224b8d` (deep blue), at ~5%–10% opacity |
| Layers | Two SVG wave paths, stacked for depth |
| Reading impact | None — waves are behind content (`z-index: -1`), extremely light |
| Language pages | Global (applies to `body`) — identical on EN `/` and ZH `/zh/` |

---

## 3. Technical Implementation

### Approach: inline SVG + SCSS (user-approved)

| Item | Decision |
|------|----------|
| New file | `_sass/_background.scss` — wave layer styles |
| Import | Add `@import "background";` to `assets/css/main.scss` (after `@import "base"`/near other layout imports) |
| SVG | Inline `<svg>` with `preserveAspectRatio="none"`, two `<path>` elements using cubic bezier `C` commands |
| Responsive | Reduce wave height on mobile via `@include breakpoint($small)` |
| z-index | `-1` so content and sidebar stay above |

### Implementation sketch

```scss
// _sass/_background.scss
.wave-background {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 22vh;              // adjust for balance
  z-index: -1;
  pointer-events: none;      // never block clicks
}
```

SVG paths (two layered waves) rendered inline in the layout or injected via an include:

```html
<svg class="wave-background" viewBox="0 0 400 180" preserveAspectRatio="none" aria-hidden="true">
  <path d="M0,90 C50,40 100,140 150,90 C200,40 250,140 300,90 C350,40 400,140 400,90 L400,180 L0,180 Z"
        fill="rgba(34,75,141,0.10)"/>
  <path d="M0,120 C50,70 100,170 150,120 C200,70 250,170 300,120 C350,70 400,170 400,120 L400,180 L0,180 Z"
        fill="rgba(34,75,141,0.07)"/>
</svg>
```

**Where to place the SVG:** must render on both EN and ZH pages. Best approach: add to `_layouts/default.html` (single layout used by both pages), or as a new include `_includes/wave-background.html` included from `default.html`. Recommend the include for isolation.

---

## 4. Files Touched

| File | Action |
|------|--------|
| `_sass/_background.scss` | **Create** — wave styles |
| `assets/css/main.scss` | **Modify** — add `@import "background";` |
| `_includes/wave-background.html` | **Create** — inline SVG markup |
| `_layouts/default.html` | **Modify** — include wave background |

---

## 5. Non-Goals (explicitly excluded)

- No animation / motion effects
- No theme color changes
- No background images
- No changes to other template styles
- No changes to page content (EN/ZH)

---

## 6. Acceptance Criteria

- [ ] Wave decoration visible at bottom of both `/` and `/zh/` pages
- [ ] Content (sidebar, text) remains readable and unaffected — waves behind content
- [ ] Waves do not intercept mouse clicks (`pointer-events: none`)
- [ ] Mobile view: waves scale correctly (`preserveAspectRatio="none"` + breakpoint)
- [ ] Site builds cleanly (`bash run_server.sh` / Jekyll build)
