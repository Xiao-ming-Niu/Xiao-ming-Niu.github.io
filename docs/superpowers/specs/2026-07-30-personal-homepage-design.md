# Personal Academic Homepage — Design Spec

**Date**: 2026-07-30
**Status**: Approved
**Scope**: Refine and complete the existing Jekyll academic homepage

---

## 1. Purpose & Audience

A comprehensive academic + professional personal homepage for Xiaoming Niu (Master's student, Computational Mathematics, Shantou University).

**Primary audiences**: potential PhD advisors, peer researchers, industry recruiters, and general visitors.

No publications section — the homepage focuses on education, projects (open source + research), honors, and skills.

---

## 2. Page Structure

### English page (`_pages/about.md`)

| Order | Section | Status |
|-------|---------|--------|
| 1 | About Me | Existing — rewrite to remove placeholder text, add specific research interests |
| 2 | Education | Existing — replace Lorem Ipsum with real timeline entries |
| 3 | Open Source Projects | **New** — GitHub project cards (DL/CV/NLP): one-line description + repo link + tech tags |
| 4 | Research Projects | **New** — scientific computing / numerical methods projects |
| 5 | Honors & Awards | Existing — replace Lorem Ipsum with real awards |
| 6 | Skills | **New** — programming languages, tools, math software |

### Chinese page (`_pages/zh.md`)

Full translation of the English page, same sections, same order. Not a shortened version.

### Navigation (`_data/navigation.yml`)

Updated to reflect the new order:
`About Me → Education → Open Source Projects → Research Projects → Honors → 中文`

Remove the empty "News" entry.

---

## 3. `_config.yml` Changes

| Key | Current | Target |
|-----|---------|--------|
| `description` | "Personal Academic Homepage" | "Master's Student in Computational Mathematics at Shantou University" |
| `author.bio` | "Student" | "M.Sc. Student in Computational Mathematics" |
| `author.employer` | (empty) | "Shantou University" |
| `author.github` | (empty) | User's GitHub username |
| `author.googlescholar` | "YOUR_GOOGLE_SCHOLAR_ID" | Real ID or empty |
| `author.orcid` | (empty) | Real ORCID or leave empty |
| `google_analytics_id` | (empty) | Optional |
| SEO verification keys | (empty) | Optional |

---

## 4. Open Source Projects Block Format

Each project entry follows this compact template:

```markdown
- **Project Name** | [GitHub](repo-url)
  - One-line description of what the project does and the tech stack
  - Tags: `PyTorch` `Computer Vision` `Image Segmentation`
```

Grouped by domain (Computer Vision, NLP, Deep Learning, etc.) if there are enough projects. Otherwise a single flat list.

---

## 5. Files Touched

| File | Action |
|------|--------|
| `_config.yml` | Update author metadata, description, social links |
| `_pages/about.md` | Rewrite content — remove Lorem Ipsum, add new sections |
| `_pages/zh.md` | Rewrite to match English page structure |
| `_data/navigation.yml` | Update nav links, remove News |

No changes to `_layouts/`, `_includes/`, `_sass/` — the template structure stays as-is.

---

## 6. Non-Goals (explicitly excluded)

- No publications / papers section
- No News/blog section
- No template/layout changes
- No new Jekyll plugins or dependencies
- No dark mode or theme switching
- Google Scholar crawler: already configured, no changes needed (just fill the real ID)

---

## 7. Acceptance Criteria

- [ ] All Lorem Ipsum / placeholder text replaced with real content
- [ ] All 6 sections present and in the agreed order on the English page
- [ ] Chinese page is a complete translation (not abbreviated)
- [ ] Navigation bar matches the section order, no dead links
- [ ] `_config.yml` author fields filled with real data
- [ ] Open Source Projects each have a description + GitHub link
- [ ] Site builds and renders correctly with `bash run_server.sh`
