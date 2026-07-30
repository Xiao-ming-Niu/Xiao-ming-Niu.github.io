# Personal Homepage Refinement — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refine the existing Jekyll academic homepage by replacing all placeholder content, adding Open Source Projects / Research Projects / Skills sections, updating navigation, and completing the Chinese translation.

**Architecture:** Content-only changes across 4 files. No template, layout, or CSS changes. The Jekyll template (AcadHomepage) remains untouched — all work is in config, pages, and navigation data.

**Tech Stack:** Jekyll (Ruby), Markdown + HTML, YAML config

## Global Constraints

- No new Jekyll plugins or dependencies
- No template/layout/CSS changes
- Content must be in English (`about.md`) and Chinese (`zh.md`) with identical structure
- Section order: About Me → Education → Open Source Projects → Research Projects → Honors → Skills
- Open Source Projects each use format: name, GitHub link, one-line description, tech tags
- Site must build cleanly with `bash run_server.sh`

---

### Task 1: Update `_config.yml` — Author Metadata & Social Links

**Files:**
- Modify: `_config.yml`

**Changes:**

- [ ] **Step 1: Update site description, author bio, employer, GitHub**

Edit `_config.yml`:

```yaml
# Change line 10
description              : "Master's Student in Computational Mathematics at Shantou University"

# Change line 26 (author.bio)
  bio              : "M.Sc. Student in Computational Mathematics"

# Change line 28 (author.employer) — currently empty
  employer         : "Shantou University"

# Change line 39 (author.github) — currently empty, fill in your GitHub username
  github           : "Xiao-ming-Niu"
```

- [ ] **Step 2: Update Google Scholar ID**

Edit `_config.yml` line 30. If you have a Google Scholar ID, replace the placeholder:

```yaml
  googlescholar    : "https://scholar.google.com/citations?user=YOUR_REAL_ID"
```

If you don't have one yet, leave it empty:

```yaml
  googlescholar    :
```

- [ ] **Step 3: Verify the file**

```bash
cd G:/GithubPage && grep -n "description\|bio\|employer\|github\|googlescholar" _config.yml | head -10
```

Check that the values match the edits above.

- [ ] **Step 4: Commit**

```bash
git add _config.yml
git commit -m "Update _config.yml with real author metadata and social links"
```

---

### Task 2: Rewrite `_pages/about.md` — English Homepage Content

**Files:**
- Modify: `_pages/about.md`

**Interfaces:**
- Produces: 6 sections matching the nav entries in Task 4

- [ ] **Step 1: Replace the entire file content**

Write `_pages/about.md`:

```markdown
---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>

I am a Master's student in Computational Mathematics at
**Shantou University**.

My research interests include **numerical methods for partial differential
equations**, **finite element methods**, **scientific computing**, and
**numerical linear algebra**.

I am currently working on [your specific research topic, e.g., adaptive finite element methods for elliptic PDEs].

<span class='anchor' id='-education'></span>

# 📖 Education

- *2025.09 - Present*, **M.Sc. in Computational Mathematics**, Shantou University
  - Supervisor: [your supervisor's name]
  - Research focus: [your specific research area]

- *2021.09 - 2025.07*, **B.Sc. in [your major, e.g., Mathematics / Applied Mathematics]**, [your undergraduate university]
  - [Optional: thesis title, GPA, or key coursework]

<span class='anchor' id='-open-source-projects'></span>

# 💻 Open Source Projects

- **[Project Name 1]** | [GitHub](https://github.com/your-username/repo-name)
  - [One-line description: what it does, key technique]
  - `PyTorch` `Computer Vision` `Image Classification`

- **[Project Name 2]** | [GitHub](https://github.com/your-username/repo-name)
  - [One-line description: what it does, key technique]
  - `Transformers` `NLP` `Text Generation`

<!-- Add more projects following the same format -->

<span class='anchor' id='-research-projects'></span>

# 🔬 Research Projects

- **[Project Name]**
  - [Brief description of the research problem, your approach, and outcomes]
  - Supervisor: [name] | [Year]

<!-- Add more research projects as needed -->

<span class='anchor' id='-honors-and-awards'></span>

# 🎖 Honors and Awards

- *[YYYY.MM]* [Award name], [issuing organization]
- *[YYYY.MM]* [Award name], [issuing organization]

<span class='anchor' id='-skills'></span>

# 🛠 Skills

- **Programming:** Python, [MATLAB / C++ / etc.]
- **Deep Learning:** PyTorch, [TensorFlow / etc.]
- **Math Tools:** [MATLAB, Mathematica, etc.]
- **Scientific Computing:** [FEniCS, Deal.II, etc.]
- **Tools:** Git, LaTeX, [others]
```

- [ ] **Step 2: Verify the frontmatter and liquid tags are intact**

```bash
cd G:/GithubPage && head -10 _pages/about.md
```

Expected: frontmatter block with `permalink: /`, `author_profile: true`, and Google Scholar liquid tags.

- [ ] **Step 3: Commit**

```bash
git add _pages/about.md
git commit -m "Rewrite about.md with all 6 sections, remove Lorem Ipsum"
```

---

### Task 3: Rewrite `_pages/zh.md` — Chinese Homepage (Full Translation)

**Files:**
- Modify: `_pages/zh.md`

**Interfaces:**
- Consumes: same 6-section structure from Task 2
- Produces: Chinese page matching English content

- [ ] **Step 1: Replace the entire file content**

Write `_pages/zh.md`:

```markdown
---
layout: archive
title: "个人主页"
permalink: /zh/
author_profile: true
---

<span class='anchor' id='about-me'></span>

# 关于我

我是**汕头大学**计算数学专业的硕士研究生。

我的研究兴趣包括**偏微分方程数值方法**、**有限元方法**、**科学计算**和**数值线性代数**。

目前正在研究：[你的具体研究课题，例如：椭圆型偏微分方程的自适应有限元方法]。

<span class='anchor' id='-education'></span>

# 📖 教育经历

- *2025.09 - 至今*, **计算数学 硕士**, 汕头大学
  - 导师：[导师姓名]
  - 研究方向：[具体研究方向]

- *2021.09 - 2025.07*, **本科**, [你的本科院校]
  - 专业：[你的本科专业]
  - [可选：毕业论文题目、GPA 或核心课程]

<span class='anchor' id='-open-source-projects'></span>

# 💻 开源项目

- **[项目名称 1]** | [GitHub](https://github.com/your-username/repo-name)
  - [一句话描述：项目做什么，核心技术]
  - `PyTorch` `计算机视觉` `图像分类`

- **[项目名称 2]** | [GitHub](https://github.com/your-username/repo-name)
  - [一句话描述：项目做什么，核心技术]
  - `Transformers` `自然语言处理` `文本生成`

<!-- 按相同格式添加更多项目 -->

<span class='anchor' id='-research-projects'></span>

# 🔬 科研项目

- **[项目名称]**
  - [简要描述研究问题、方法和成果]
  - 指导老师：[姓名] | [年份]

<!-- 按需添加更多科研项目 -->

<span class='anchor' id='-honors-and-awards'></span>

# 🎖 荣誉奖项

- *[YYYY.MM]* [奖项名称]，[颁发机构]
- *[YYYY.MM]* [奖项名称]，[颁发机构]

<span class='anchor' id='-skills'></span>

# 🛠 技能

- **编程语言:** Python, [MATLAB / C++ / 等]
- **深度学习:** PyTorch, [TensorFlow / 等]
- **数学工具:** [MATLAB, Mathematica, 等]
- **科学计算:** [FEniCS, Deal.II, 等]
- **工具:** Git, LaTeX, [其他]
```

- [ ] **Step 2: Verify frontmatter is correct**

```bash
cd G:/GithubPage && head -7 _pages/zh.md
```

Expected: `layout: archive`, `permalink: /zh/`, `author_profile: true`.

- [ ] **Step 3: Commit**

```bash
git add _pages/zh.md
git commit -m "Rewrite zh.md as full Chinese translation matching English page structure"
```

---

### Task 4: Update Navigation

**Files:**
- Modify: `_data/navigation.yml`

**Interfaces:**
- Consumes: section anchors from Tasks 2 and 3 (`#about-me`, `#-education`, etc.)

- [ ] **Step 1: Replace the entire file content**

Write `_data/navigation.yml`:

```yaml
# main links links
main:
  - title: "About Me"
    url: "/#about-me"

  - title: "Education"
    url: "/#-education"

  - title: "Open Source"
    url: "/#-open-source-projects"

  - title: "Research"
    url: "/#-research-projects"

  - title: "Honors"
    url: "/#-honors-and-awards"

  - title: "中文"
    url: "/zh/"
```

- [ ] **Step 2: Verify anchors match section IDs in about.md**

```bash
cd G:/GithubPage && grep 'class=.anchor' _pages/about.md
```

Expected output should include all anchors referenced in nav: `about-me`, `-education`, `-open-source-projects`, `-research-projects`, `-honors-and-awards`.

- [ ] **Step 3: Commit**

```bash
git add _data/navigation.yml
git commit -m "Update navigation to match new section order, remove empty News"
```

---

### Task 5: Build & Verify

**Files:**
- Verify: all 4 modified files

- [ ] **Step 1: Build the site locally**

```bash
cd G:/GithubPage && bash run_server.sh
```

(If you don't have Jekyll installed locally, skip to Step 2.)

- [ ] **Step 2: Check for broken anchors**

```bash
cd G:/GithubPage && grep -oP 'id='\''[^'\'']+'\''' _pages/about.md _pages/zh.md | sort
```

Verify all anchor IDs match the URLs in `_data/navigation.yml`.

- [ ] **Step 3: Check no Lorem Ipsum remains**

```bash
cd G:/GithubPage && grep -ri "lorem" _pages/ _config.yml _data/ 2>/dev/null
```

Expected: no output (no matches).

- [ ] **Step 4: Check no placeholder Google Scholar ID**

```bash
cd G:/GithubPage && grep "YOUR_GOOGLE_SCHOLAR" _config.yml
```

Expected: no output (replaced or removed).

- [ ] **Step 5: Final commit (if any fixes from verification)**

```bash
git status
# If clean, done. If fixes were made:
git add -A
git commit -m "Fix issues found during verification"
```
