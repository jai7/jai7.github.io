# Portfolio

Personal portfolio built with [Astro](https://astro.build), deployed to GitHub Pages.

## Prerequisites

- Node.js v24+
- npm

## Setup

```bash
npm install
```

## Making a change

Content lives in `src/content/` as Markdown files, organized by section:

| Section | Directory | Required frontmatter |
|---|---|---|
| Thoughts (blog posts) | `src/content/thoughts/` | `title`, `date` |
| Projects | `src/content/projects/` | `title`, `date` |
| Experiments | `src/content/experiments/` | `title`, `date` |
| Questions | `src/content/questions/` | `question` |

### Adding a thought

Create a file at `src/content/thoughts/YYYY-MM-DD-slug.md`:

```markdown
---
title: Your post title
date: 2026-05-12
tags: [tag1, tag2]
description: One-line summary shown in the listing.
readingTime: 5 min read
---

Post body here.
```

### Adding a project

Create a file at `src/content/projects/YYYY-MM-DD-slug.md`:

```markdown
---
title: Project name
date: 2026-05-12
tags: [infra]
status: shipped        # ongoing | shipped | archived
description: One-line summary.
tech: Go · Postgres
---

Project body here.
```

### Adding a question

Create a file at `src/content/questions/slug.md`:

```markdown
---
question: What is the question you want to explore?
category: General
---
```

## Build and verify locally

Start the dev server with hot reload:

```bash
npm run dev
```

Open [http://localhost:4321](http://localhost:4321) and verify your changes.

To do a production build and preview it locally:

```bash
npm run build
npm run preview
```

`preview` serves the `dist/` output at [http://localhost:4321](http://localhost:4321) — same as what GitHub Pages will serve.

## Publish

Push to `main`:

```bash
git add src/content/...
git commit -m "feat: add <title>"
git push
```

The [deploy workflow](.github/workflows/deploy.yml) runs automatically on every push to `main`. It type-checks with `astro check`, builds, and deploys to GitHub Pages. Monitor progress at the **Actions** tab in the GitHub repo.
