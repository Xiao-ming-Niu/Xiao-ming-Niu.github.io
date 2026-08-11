# Background Wave Decoration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a subtle fixed-bottom two-layer SVG wave decoration to the page background, visible on both EN and ZH pages.

**Architecture:** An inline SVG include (`_includes/wave-background.html`) rendered by the shared layout (`default.html`), styled by a new SCSS partial (`_sass/_background.scss`) imported into the main stylesheet. Pure CSS/HTML — no JS, no images, no dependencies.

**Tech Stack:** SCSS, Jekyll Liquid includes, inline SVG

## Global Constraints

- No animation / motion effects
- No theme color changes — wave color uses `#224b8d` (deep blue) at 5%–10% opacity
- No background images
- No changes to page content (EN/ZH `_pages/*`)
- Waves behind content: `z-index: -1`
- Waves must not intercept clicks: `pointer-events: none`
- Applies to both `/` and `/zh/` pages (global via layout)

---

### Task 1: Create the wave background include (SVG)

**Files:**
- Create: `_includes/wave-background.html`

**Interfaces:**
- Produces: HTML fragment with class `wave-background` that Task 2's SCSS styles and Task 3's layout consumes

- [ ] **Step 1: Create the include file**

Write `_includes/wave-background.html`:

```html
<!-- Two-layer wave decoration, fixed at the bottom of the viewport -->
<svg class="wave-background" viewBox="0 0 400 180" preserveAspectRatio="none" aria-hidden="true">
  <path d="M0,90 C50,40 100,140 150,90 C200,40 250,140 300,90 C350,40 400,140 400,90 L400,180 L0,180 Z"
        fill="rgba(34,75,141,0.10)"/>
  <path d="M0,120 C50,70 100,170 150,120 C200,70 250,170 300,120 C350,70 400,170 400,120 L400,180 L0,180 Z"
        fill="rgba(34,75,141,0.07)"/>
</svg>
```

- [ ] **Step 2: Verify the file**

```bash
cd G:/GithubPage && cat _includes/wave-background.html
```

Expected: the SVG with class `wave-background`, two paths, fills `rgba(34,75,141,0.10)` and `rgba(34,75,141,0.07)`, `preserveAspectRatio="none"`, `aria-hidden="true"`.

- [ ] **Step 3: Commit**

```bash
git add _includes/wave-background.html
git commit -m "feat: add wave background SVG include"
```

---

### Task 2: Add wave stylesheet and import it

**Files:**
- Create: `_sass/_background.scss`
- Modify: `assets/css/main.scss` (add import line)

**Interfaces:**
- Consumes: `wave-background` class from Task 1's SVG
- Produces: `.wave-background` CSS rules (Task 3's layout renders the element they target)

- [ ] **Step 1: Create the SCSS partial**

Write `_sass/_background.scss`:

```scss
/* ==========================================================================
   BACKGROUND WAVE DECORATION
   ========================================================================== */

.wave-background {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 22vh;
  z-index: -1;
  pointer-events: none;

  /* On small screens, reduce wave height so content has more room */
  @include breakpoint($small) {
    height: 12vh;
  }
}
```

- [ ] **Step 2: Import the partial in the main stylesheet**

Edit `assets/css/main.scss` — insert the import after `@import "page";` and before `@import "archive";`:

```scss
@import "page";
@import "background";
@import "archive";
```

- [ ] **Step 3: Verify the SCSS compiles**

```bash
cd G:/GithubPage && ruby -e "require 'sassc'; engine = SassC::Engine.new(File.read('_sass/_background.scss'), syntax: :scss); puts engine.render"
```

If Ruby/SassC is not available, verify with Jekyll build instead (or skip to Task 3's layout verification and build in Task 4).

Expected: no errors; rendered CSS contains `.wave-background` rules with `position: fixed` and `z-index: -1`.

- [ ] **Step 4: Commit**

```bash
git add _sass/_background.scss assets/css/main.scss
git commit -m "feat: add wave background styles and import"
```

---

### Task 3: Render the wave in the shared layout

**Files:**
- Modify: `_layouts/default.html`

**Interfaces:**
- Consumes: `_includes/wave-background.html` (Task 1), `.wave-background` styles (Task 2)
- Produces: wave visible on every page using the default layout (both `/` and `/zh/`)

- [ ] **Step 1: Add the include to the layout**

Edit `_layouts/default.html` — add the include right after `<body>` opening tag:

```html
  <body>

    {% include wave-background.html %}
    {% include browser-upgrade.html %}
    {% include masthead.html %}
```

- [ ] **Step 2: Verify the layout renders the include**

```bash
cd G:/GithubPage && grep -n "wave-background" _layouts/default.html
```

Expected: one line — `{% include wave-background.html %}`.

- [ ] **Step 3: Commit**

```bash
git add _layouts/default.html
git commit -m "feat: render wave background in default layout"
```

---

### Task 4: Build and verify

**Files:**
- Verify: all 4 files from Tasks 1–3

- [ ] **Step 1: Build the site**

```bash
cd G:/GithubPage && bash run_server.sh
```

(If the Jekyll environment is unavailable locally, skip to Step 2 and verify structurally.)

- [ ] **Step 2: Verify wave element present in rendered output**

Check that the include appears in the generated page (look in `_site/` after a build):

```bash
cd G:/GithubPage && grep -rl "wave-background" _site/ 2>/dev/null | head -5
```

Expected: at least `_site/index.html` and `_site/zh/index.html` contain `wave-background`.

- [ ] **Step 3: Verify no regression in page content**

```bash
cd G:/GithubPage && grep -rn "lorem" _pages/ 2>/dev/null
```

Expected: no output (no placeholder text reintroduced).

- [ ] **Step 4: Final commit if fixes were needed**

```bash
git status
# If clean, done. If fixes were made:
git add -A
git commit -m "fix: issues found during verification"
```
