# kays0x fork

Personal fork of [Digital-Process-Tools/claude-remember](https://github.com/Digital-Process-Tools/claude-remember), used under its Community License (personal and internal modification). Branch `kevin` carries the changes; `main` tracks upstream.

## Changes

| File | Change |
| --- | --- |
| `scripts/save-session.sh` | `--recover`: bypasses the minimum-message gates, honors the cooldown. |
| `scripts/session-start-hook.sh` | Recovers a previous session whose saved position is behind its transcript, using `--recover` instead of `--force`. |
| `scripts/lib-memory-context.sh` | `archive.md` is not injected at session start. It stays on disk for search. |

Each change is marked with a `KEVIN FORK` comment.

## Install

This repo is its own marketplace (`.claude-plugin/marketplace.json`, name `kays0x`):

```bash
claude plugin marketplace add <path-to-this-checkout>
claude plugin install remember@kays0x
```

After a commit, bump `version` in `.claude-plugin/plugin.json` (`<upstream>-kays0x.<n>`), then run `claude plugin marketplace update kays0x && claude plugin update remember@kays0x`.

## Merging upstream

1. `git fetch upstream --tags && git merge <tag>` on `kevin`; resolve around the `KEVIN FORK` blocks.
2. Run the suite on the upstream tag and on `kevin`. Tests failing only on `kevin` must match `fork-expected-failures.txt` (tests that assert archive injection or a `--force` recovery). Update the list when upstream adds or renames such tests.
3. Set the version to `<tag>-kays0x.1` and reinstall.
