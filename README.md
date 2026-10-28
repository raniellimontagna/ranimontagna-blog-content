# ranimontagna-blog-content

Blog posts for [ranimontagna.com/blog](https://ranimontagna.com/blog), written in MDX in Portuguese, English and Spanish.

**Live:** https://ranimontagna.com/blog

This repository holds content only. The portfolio ([ranimontagna.com](https://github.com/raniellimontagna/ranimontagna.com)) reads it at runtime through the GitHub API, so publishing a post does not need a new deploy.

## Structure

```text
posts/
├── pt/    # Portuguese (main language)
├── en/    # English translations
└── es/    # Spanish translations
docs/
└── superpowers/    # Writing specs and plans for individual posts
```

## Writing a post

### File name

```text
posts/<locale>/YYYY-MM-DD-<slug>.mdx
```

The slug must be identical in every language so the blog can link the translations of a post:

```text
posts/pt/2026-06-04-agent-toolkit-workflows-ia-terminal.mdx
posts/en/2026-06-04-agent-toolkit-workflows-ia-terminal.mdx
posts/es/2026-06-04-agent-toolkit-workflows-ia-terminal.mdx
```

Files that do not match this pattern are ignored.

### Frontmatter

```mdx
---
title: 'Agent Toolkit: my AI setup for turning the terminal into an agent workspace'
date: '2026-06-04'
description: >-
  I built an open-source installer to configure Claude Code, Codex CLI,
  OpenCode, Gemini CLI, Graphify, GSD and my development skills with one
  command.
tags:
  - ai
  - agent-toolkit
  - open-source
published: true
coverImage: >-
  https://cdn.ranimontagna.com/blog/fe83cd58-9e23-41cc-9d37-2ab92ebd7cf2.webp
---

Post body in Markdown...
```

| Field | Required | Rules |
| --- | --- | --- |
| `title` | yes | Up to 200 characters |
| `date` | no | `YYYY-MM-DD`. Defaults to the date in the file name |
| `description` | yes | Up to 600 characters |
| `tags` | no | Up to 20 tags, 40 characters each |
| `published` | yes | `true` or `false` |
| `coverImage` | no | An `https` URL on `cdn.ranimontagna.com`, `media.ranimontagna.com` or `images.unsplash.com`, or a path relative to the blog media base URL. Without it, a default image is used |

Any other frontmatter key makes the post invalid.

### Content rules

The portfolio validates every post before it is cached and skips posts that break these rules:

- Write plain Markdown with GitHub Flavored Markdown (tables, task lists, strikethrough). Raw HTML, JSX components, `import`/`export` and `{expressions}` are rejected.
- Links and images must be relative paths, `#anchors`, `https:` or `mailto:` URLs.
- The body is limited to 500,000 characters.

Code blocks tagged `mermaid` render as diagrams.

A post is visible only when `published: true` and its `date` is today or earlier, so a future date schedules it.

## How publishing works

1. A commit lands in this repository, either from the private admin panel (which writes through the GitHub API) or from a direct push.
2. A GitHub webhook on `push` calls `POST https://ranimontagna.com/api/revalidate`, signed with a shared secret (`X-Hub-Signature-256`).
3. The route invalidates the `posts` cache tag in Next.js and bumps the blog cache version in Redis.
4. The next visit reads the updated posts from this repository through the GitHub API.

If the webhook fails, changes still appear once the portfolio's caches expire.
