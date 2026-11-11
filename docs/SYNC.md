# Sync operations

## Scheduled tasks

- `MinGLonG Skills Watcher` runs at logon and watches the local skills directory. Local edits are debounced for about 12 seconds, then committed and pushed.
- `MinGLonG Skills Periodic Sync` runs every 30 minutes as a fallback and pulls remote changes even when no local file event occurs.
- The watcher also performs a reconciliation every 15 minutes.

## Logs

- `%USERPROFILE%\.agents\watch-skills.log`
- `%USERPROFILE%\.agents\sync-skills.log`

## Manual sync

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File "$env:USERPROFILE\.agents\sync-skills.ps1"
```

## Conflict policy

The sync never force-pushes. If remote and local history both changed, it uses rebase. On conflict it aborts the rebase, keeps the local commit, and logs the error for manual resolution.

## Adding a skill

Create a new directory directly under `%USERPROFILE%\.agents\skills`, with a valid `SKILL.md` at its root. The watcher will commit and push it automatically.