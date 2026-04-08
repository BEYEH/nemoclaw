---
description: "Stage and commit changes. Leave argument empty to commit all, or specify file paths to commit selectively."
agent: "agent"
argument-hint: "File paths to commit (leave empty for all changes)"
---

Commit workflow:

**If `{argument}` is provided** (specific files):

1. `git diff -- {argument}` to review changes
2. `git add -- {argument}`
3. Craft commit message from the diff

**If `{argument}` is empty** (all changes):

1. `git status` then `git diff` to review all changes
2. `git add -A`
3. Craft commit message from the diff

Commit message rules (Conventional Commits):

**Header** (required): `<type>(<scope>): <subject>`

- `type`: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `revert`
- `scope`: affected area, e.g. `frontend`, `backend`, `database` (optional)
- `subject`: short description, ≤ 50 chars, sentence case, no period

**Body** (optional): explain _why_, not _what_; ≤ 72 chars per line.
Only include for significant changes or important decisions.

**Footer** (optional): task ID or `BREAKING CHANGE: <description>`.

Commit locally only, do not push.
