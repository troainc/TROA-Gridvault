# Command reference

Commands below run in Space Engineers in-game chat. Replace `<placeholder>` text with a value; do not type the angle brackets. `!gridvault help` displays in-game help. Only server administrators can use admin operations.

## Players

| Command | Purpose |
|---|---|
| `!gridvault help` | Show command guidance. |
| `!gridvault mine` | List your observed grid history and available metadata. |
| `!gridvault request <grid-name-or-id> [revision]` | Ask staff to restore your grid. Approval is required. Quote names with spaces. |
| `!gridvault category <grid-name-or-id> <Ship\|Base\|Mining\|Combat\|Other\|None>` | Label a grid-history entry. |

## Server administrators

| Command | Purpose |
|---|---|
| `!gridvault help` | Show help. |
| `!gridvault reload` | Reload config without restarting Torch. |
| `!gridvault overview` | Show backup queue and settings. |
| `!gridvault storeall` / `!gridvault run` / `!gridvault archive` | Start a normal qualifying backup pass. |
| `!gridvault save` | Back up the grid you are looking at. |
| `!gridvault capture <grid-id>` | Back up one grid by entity ID. |
| `!gridvault backupworld confirm` | Start an exceptional full-world pass that bypasses normal filters and quotas. Review the warning first. |
| `!gridvault safeguard` | Start a backup pass before an external restart. |
| `!gridvault precleanup` | Start a pass before external cleanup. |
| `!gridvault prewipe [note]` | Write a pre-wipe report and start a pass. |
| `!gridvault find <name-or-id>` | Search vaults; supports `*` and `?`. Quote names with spaces. |
| `!gridvault list <player-or-steamid> [grid]` | List one player's grids or a grid's numbered revisions (`1` is newest). |
| `!gridvault list faction <tag> [grid]` | List faction grids or revisions. |
| `!gridvault records <steam-id> [grid]` | View grid history and revisions. |
| `!gridvault preview <steam-id> <grid-id> [revision]` | Inspect a backup and its original GPS before restore. |
| `!gridvault restore <player-or-steamid> <grid> [revision] [keepOriginalPos] [force]` | Restore onto its owner. See [Recovery](RECOVERY.md) for flags and safety. |
| `!gridvault restore faction <tag> <grid> [revision] [keepOriginalPos] [force]` | Restore faction grid onto its owner. |
| `!gridvault recover <steam-id> <grid-id> [revision]` | Restore near the in-game admin. |
| `!gridvault recoverat <steam-id> <grid-id> <x> <y> <z> [revision]` | Restore at exact GPS coordinates. |
| `!gridvault recoverorigin <steam-id> <grid-id> [revision]` | Restore at saved coordinates when safe. |
| `!gridvault audit <steam-id>` | Verify hashes and SBC readability in the background. |
| `!gridvault health` | Show storage usage, incomplete entries, and pending writes. |
| `!gridvault clearup [confirm]` | Remove expired backups after the confirmation flow. |
| `!gridvault export <steam-id>` | Export a player vault for transfer. |
| `!gridvault import <steam-id> <folder-name>` | Import a staged transfer. |
| `!gridvault requests` | List pending player recovery requests. |
| `!gridvault approve <request-id> <x> <y> <z>` | Approve and deploy a requested grid at coordinates. |
| `!gridvault reject <request-id>` | Reject a recovery request. |
| `!gridvault webhook` / `!gridvault webhook test` | Inspect or test audit delivery. |

## Discord command bridge

Gridvault+ does not create Discord slash commands or a Discord chat relay. A server may use an existing secured Torch command bridge to forward supported administrator commands, for example `!gridvault recoverat <steam-id> <grid-id> <x> <y> <z>`. Restrict this route to trusted staff. Never expose player/admin data in a public channel. Gridvault+ audit embeds are sent directly by its own webhook and do not depend on Monitor+.
