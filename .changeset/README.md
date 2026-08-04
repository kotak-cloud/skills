# Changesets

Every change to a skill ships as a changeset — a markdown file in this directory. On merge to `main`, the Release workflow turns pending changesets into a version bump, a `CHANGELOG.md` entry, and a git tag.

## Adding a changeset

```bash
npx changeset
```

or write the file by hand:

```markdown
---
"kotak-cloud-skills": minor
---

Describe the change: what the skill does differently now, and why.
```

## Bump rules

- `minor` — a skill gains or changes behavior (the common case).
- `patch` — a plain bugfix to a skill.
- `major` — breaking change to how a skill is invoked or installed.
