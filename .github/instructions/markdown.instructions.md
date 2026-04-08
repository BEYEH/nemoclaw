---
description: "Use when creating or editing README.md or any Markdown file. Covers TOC, headings, links, lists, code blocks, and formatting conventions for this knowledge base."
applyTo: "**/*.md"
---

# Markdown Conventions

## File Structure

Every README must follow this header order:

```markdown
<!-- omit in toc -->

# Title

<!-- omit in toc -->

## Table of contents

- [Section](#section)

## Section
```

## Rules

- Place `<!-- omit in toc -->` before H1 and `## Table of contents`
- Use relative links (e.g., `./subfolder/README.md`), avoid absolute paths
- Bullet lists use `- ` (not `*`)
- H2 for major sections, H3 for subsections

## Tips and Notes

- Use `- **Label**：description` for tips, notes, and warnings — not blockquotes
- Reserve blockquotes (`>`) for quoting external content or critical warnings only
- Code blocks under a list item must be indented with 2 spaces

## Code Blocks

- Always specify language after triple backtick (e.g., ` ```text `, ` ```bash `, ` ```markdown `)
- Use `text` for free-form content, not a blank or space after the backtick
- Do not place blank lines between consecutive blockquotes (MD028)
