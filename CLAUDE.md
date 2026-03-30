# CLAUDE.md — AI Assistant Guide for rohitk09.github.io

This file documents the codebase structure, development workflows, and conventions for AI assistants working on this repository.

---

## Project Overview

This is a **Jekyll-based personal academic/professional website** hosted on GitHub Pages. It is built on the [Academic Pages](https://github.com/academicpages/academicpages.github.io) template, which extends the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) Jekyll theme.

- **Owner:** Rohit Katyal
- **Live URL:** https://rohitk09.github.io
- **Repository:** RohitK09/rohitk09.github.io
- **Theme:** Academic Pages (fork of Minimal Mistakes)
- **Framework:** Jekyll (static site generator)
- **Hosting:** GitHub Pages (auto-deploys on push to `master`)

---

## Directory Structure

```
rohitk09.github.io/
├── _config.yml          # Main site configuration (title, author info, plugins, etc.)
├── Gemfile              # Ruby gem dependencies for Jekyll
├── _data/               # Structured YAML/JSON data files
│   ├── navigation.yml   # Header navigation links
│   ├── cv.json          # CV data for the JSON-generated CV page
│   ├── authors.yml      # Co-author profiles for multi-author posts
│   └── ui-text.yml      # Localization strings for the theme UI
├── _pages/              # Single standalone pages (About, CV, Publications list, etc.)
├── _posts/              # Blog posts (YYYY-MM-DD-title.md)
├── _publications/       # Individual publication entries
├── _talks/              # Individual talk/presentation entries
├── _teaching/           # Individual teaching experience entries
├── _portfolio/          # Individual portfolio/project entries
├── _drafts/             # Unpublished draft posts (not included in build)
├── _includes/           # Reusable HTML snippets (header, footer, sidebars, etc.)
├── _layouts/            # Page layout templates
├── _sass/               # SCSS/Sass stylesheets
├── assets/              # Compiled CSS, JavaScript, fonts
├── images/              # Image files (profile photo, post images, etc.)
├── files/               # Static files for download (PDFs, slides, bibtex, etc.)
├── markdown_generator/  # Jupyter notebooks to generate Markdown from CSV data
├── talkmap/             # Leaflet.js map of talk locations
├── talkmap.ipynb        # Notebook to regenerate the talk map
├── talkmap.py           # Python script version of the talk map generator
└── scripts/             # Utility scripts
```

---

## Key Configuration Files

### `_config.yml`
The primary site configuration. Key fields to update:
- `title`, `name`, `description` — site identity
- `author.*` — sidebar author profile (bio, location, avatar, social links)
- `publication_category` — categories for grouping publications
- `analytics.provider` / `analytics.google.tracking_id` — Google Analytics setup
- `comments.provider` — comment system (Disqus, Staticman, etc.)

Changes to `_config.yml` require a server restart (`bundle exec jekyll serve`).

### `_data/navigation.yml`
Controls the top navigation bar. Add, remove, or reorder sections here.

### `_data/cv.json`
Structured JSON used by the `/cv-json/` page. The Markdown-based `/cv/` page (`_pages/cv.md`) is used by default.

---

## Content Collections

Each collection maps to a directory of Markdown files. All files use YAML front matter.

### Publications (`_publications/`)
```yaml
---
title: "Paper Title"
collection: publications
category: manuscripts  # manuscripts | conferences | books
permalink: /publication/YYYY-MM-DD-short-title
excerpt: 'One-sentence summary.'
date: 2024-01-01
venue: 'Journal or Conference Name'
paperurl: '/files/paper.pdf'   # optional
slidesurl: '/files/slides.pdf' # optional
bibtexurl: '/files/paper.bib'  # optional
citation: 'Author. (Year). "Title." <i>Venue</i>.'
---
Abstract or description here.
```

### Talks (`_talks/`)
```yaml
---
title: "Talk Title"
collection: talks
type: "Talk"  # Talk | Tutorial | Poster | Keynote | Invited Talk
permalink: /talks/YYYY-MM-DD-short-title
venue: "Institution or Conference"
date: 2024-01-01
location: "City, Country"
---
Description here.
```

### Teaching (`_teaching/`)
```yaml
---
title: "Course Name"
collection: teaching
type: "Undergraduate course"  # or Graduate seminar, Workshop, TA, etc.
permalink: /teaching/YYYY-term-course-name
venue: "University, Department"
date: 2024-01-01
location: "City, Country"
---
Course description here.
```

### Portfolio (`_portfolio/`)
```yaml
---
title: "Project Name"
excerpt: "Short description. <br/><img src='/images/project.png'>"
collection: portfolio
---
Full project description here.
```

### Blog Posts (`_posts/`)
```yaml
---
title: 'Post Title'
date: 2024-01-01
permalink: /posts/YYYY/MM/post-slug/
tags:
  - tag1
  - tag2
---
Post content here.
```

---

## File Naming Conventions

| Collection     | Pattern                          | Example                            |
|----------------|----------------------------------|------------------------------------|
| `_posts/`      | `YYYY-MM-DD-slug.md`             | `2024-03-15-my-new-post.md`        |
| `_publications/` | `YYYY-MM-DD-short-title.md`   | `2024-01-10-my-paper.md`           |
| `_talks/`      | `YYYY-MM-DD-short-title.md`      | `2024-06-01-icml-talk.md`          |
| `_teaching/`   | `YYYY-term-course.md`            | `2023-fall-cs101.md`               |
| `_portfolio/`  | `descriptive-name.md` or `.html` | `ml-project.md`                    |

---

## Static Assets

- **Profile image:** `images/profile.png` (referenced in `_config.yml`)
- **Downloadable files** (PDFs, slides): place in `/files/` — accessible at `https://rohitk09.github.io/files/filename.pdf`
- **Post/portfolio images:** place in `/images/`

---

## Development Workflow

### Local Setup
```bash
# Install Ruby dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve -l -H localhost
# Site available at http://localhost:4000

# Or use Docker
docker-compose up
```

### Deployment
Pushing to the `master` branch triggers automatic deployment via GitHub Pages. No CI/CD configuration is needed beyond this.

### Branch Strategy
- `master` — production branch, auto-deployed to GitHub Pages
- Feature branches — use for drafts or experimental changes before merging to `master`

---

## Markdown & Content Features

- **Math:** Use `$$...$$` for display math and `\\(...\\)` for inline math (MathJax v3)
- **Diagrams:** Use fenced code blocks with ` ```mermaid ` (Mermaid v11)
- **Charts:** Use fenced code blocks with ` ```plotly ` (JSON data, Plotly.js)
- **Emoji:** Supported via the `jemoji` plugin, e.g. `:computer:`
- **Notices/callouts:** Append `{: .notice}` to a paragraph
- **Collapsible sections:** Use HTML `<details>` and `<summary>` tags

---

## Talk Map

The `talkmap.html` page (`_pages/talkmap.html`) shows an interactive map of all talk locations.

To regenerate after adding talks:
```bash
python talkmap.py
# or run the talkmap.ipynb notebook
```

To enable the link to the talk map from the Talks page, set `talkmap_link: true` in `_config.yml`.

---

## Markdown Generator

The `markdown_generator/` directory contains Jupyter notebooks that convert CSV spreadsheets into properly-formatted Markdown files for publications and talks:

- `publications.ipynb` / `publications.py` — from `publications.tsv`
- `talks.ipynb` / `talks.py` — from `talks.tsv`

Workflow: update the TSV → run the notebook → commit generated Markdown files.

---

## CV Options

Two CV formats are available:

1. **Markdown CV** (`_pages/cv.md`) — manually edited, rendered at `/cv/` — **this is the default**
2. **JSON CV** (`_pages/cv-json.md`) — generated from `_data/cv.json`, rendered at `/cv-json/`

Switch between them in `_data/navigation.yml` by commenting/uncommenting the respective link.

---

## Common Tasks

### Add a new publication
1. Create `_publications/YYYY-MM-DD-title.md` with required front matter
2. (Optional) place PDF in `/files/`
3. Commit and push to `master`

### Add a new blog post
1. Create `_posts/YYYY-MM-DD-title.md`
2. Set `title`, `date`, `permalink`, and `tags` in front matter
3. Commit and push

### Update the sidebar profile
Edit `_config.yml` under the `author:` section. Changes take effect after restart.

### Change navigation links
Edit `_data/navigation.yml`. Changes are live after next build.

### Add Google Analytics
1. Set `analytics.provider: "google-analytics-4"` in `_config.yml`
2. Set `analytics.google.tracking_id: "G-XXXXXXXXXX"`

---

## Key Conventions

1. **Do not commit `_site/`** — it is gitignored; GitHub Pages builds it automatically.
2. **Don't edit files in `assets/js/plugins/` or `assets/js/vendor/`** — these are third-party.
3. **Collection files are the source of truth** — the CV, Publications, Talks pages auto-render from `_publications/`, `_talks/`, `_teaching/` directories.
4. **Permalink uniqueness** — every content file must have a unique `permalink` in front matter.
5. **Date format** — use `YYYY-MM-DD` in front matter; the filename date only affects sort order.
6. **Images** — keep in `/images/`; reference as `/images/filename.png` (absolute path).
7. **PDFs and downloads** — keep in `/files/`; reference as `/files/filename.pdf`.
