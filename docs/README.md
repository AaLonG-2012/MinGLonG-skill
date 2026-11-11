# MinGLonG Skill Repository

This repository is the source of truth for locally installed agent skills.

## Layout

Each top-level directory is one skill bundle and must contain a `SKILL.md` file:

```text
<skill-name>/
  SKILL.md
  references/
  scripts/
  assets/
```

## Windows sync

The local working copy is `%USERPROFILE%\.agents\skills`.
A background watcher commits and pushes local changes, pulls remote updates, and runs a periodic reconciliation every 15 minutes. A separate scheduled task performs a fallback sync every 30 minutes.

Conflicts are never force-pushed. If local and remote edits conflict, the local commit is kept and the error is written to `sync-skills.log` for manual resolution.
