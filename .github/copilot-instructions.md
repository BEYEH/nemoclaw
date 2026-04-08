# Copilot Instructions

## Core Rules

- **Always reuse existing code — no redundancy.**
- **Language: Always respond in 繁體中文. Technical terms remain in English.**
- **Environment: Ubuntu Linux. All terminal commands must work in bash.**

## Naming Conventions

- **Folders**: kebab-case English (e.g., `docs/network-policy`, `nemoclaw-blueprint`)

## Markdown Conventions

- Place `<!-- omit in toc -->` before H1 title and the `## Table of contents` heading
- Every README must include a TOC section
- Use relative links with `./` prefix
- Bullet lists use `- ` (not `*`)

## Git Commit Conventions

Format: `<type>(<scope>): <subject>`

- **type**: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `revert`
- **scope**: affected area, e.g. `career`, `technique`, `company` (optional)
- **subject**: ≤ 50 chars, sentence case, no period
- **Body**: explain _why_; ≤ 72 chars/line; only for significant changes (optional)
- **Footer**: task ID or `BREAKING CHANGE: <description>` (optional)
