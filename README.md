# TROA-Gridvault

## Modern Grid Backup and Recovery for Space Engineers Torch Servers

TROA-Gridvault is a no-UI, command-driven Torch plugin that protects Space Engineers grids with scheduled backups, Steam-ID-first storage, safe recovery tools, player recovery requests, and optional Discord audit embeds.

This public repository contains **release packages and documentation only**. Source code, private configuration, server data, and webhook URLs are not included.

## Why Use Gridvault

- **Steam-ID-first backups** — player backup folders remain useful after world wipes and Keen identity changes.
- **Readable files** — each backup is stored in a timestamp folder and uses the grid's full name as the SBC filename.
- **Safer recovery** — preview a backup before restoring it, then restore near an admin, at exact GPS coordinates, or at the saved location.
- **Collision protection** — restores use a conservative grid-size safety radius and refuse locations that are occupied.
- **Player requests** — players can view their own backups and ask staff for a restore without receiving admin rights.
- **Audit-ready** — optional Discord embeds track backups, restores, verification, failures, and player requests.
- **Host friendly** — designed for Windows, Linux, and AMP-hosted Torch servers; no desktop UI required.

## Requirements

- A working Space Engineers Torch server.
- .NET Framework 4.8-compatible Torch runtime.
- Server administrator access for setup and recovery commands.
- A private Discord webhook only if audit embeds are desired.

## Install

1. Download the newest `TROAGridVault-v*.zip` from this repository's releases.
2. Stop Torch or unload the old Gridvault package.
3. Install the plugin package using your host's normal Torch plugin process.
4. Start Torch once; it creates `TROAGridVault.cfg` with explanations for every setting.
5. Edit the config, save it, and use `!gridvault reload` in game.
6. Test `!gridvault storeall`, `!gridvault records <steam-id>`, and a safe non-production recovery before relying on it live.

## Backup Folder Layout

```text
TROAGridVaultBackups/
  Players/<steam-id-64>/<utc-timestamp>/<full-grid-name>.sbc
  KeenIdentities/<keen-identity-id>/<utc-timestamp>/<full-grid-name>.sbc
  Unowned/<utc-timestamp>/<full-grid-name>.sbc
  RestoreRequests/
```

- `Players` is the preferred location for player-owned grids.
- `KeenIdentities` is used when a grid has a Keen identity but no resolved Steam owner.
- `Unowned` contains truly ownerless grids.
- Existing older backup folders remain readable and are not moved automatically.

## Commands

### Players

| Command | Use |
|---|---|
| `!gridvault mine` | Lists the player's own backups. |
| `!gridvault request <grid-id> [revision]` | Requests recovery of a backed-up grid; staff approval is required. |

### Server Administrators

| Command | Use |
|---|---|
| `!gridvault help` | Shows command help in game. |
| `!gridvault reload` | Reloads configuration without restarting Torch. |
| `!gridvault overview` | Shows backup queue and settings. |
| `!gridvault storeall` | Backs up qualifying server grids. |
| `!gridvault archive` | Alias for `storeall`. |
| `!gridvault safeguard` | Starts a backup pass before an external restart. |
| `!gridvault capture <grid-id>` | Backs up one grid immediately. |
| `!gridvault records <steam-id> [grid]` | Lists grid history and revisions. |
| `!gridvault preview <steam-id> <grid-id> [revision]` | Shows backup details and original GPS. |
| `!gridvault audit <steam-id>` | Verifies backup hashes and SBC readability. |
| `!gridvault health` | Shows storage usage, incomplete entries, and pending writes. |
| `!gridvault recover <steam-id> <grid-id> [revision]` | Restores near an in-game admin. |
| `!gridvault recoverat <steam-id> <grid-id> <x> <y> <z> [revision]` | Restores at exact GPS coordinates; suitable for a Discord-to-Torch bridge. |
| `!gridvault recoverorigin <steam-id> <grid-id> [revision]` | Restores at the saved location when it is clear. |
| `!gridvault requests` | Lists player recovery requests. |
| `!gridvault approve <request-id> <x> <y> <z>` | Approves and deploys a requested grid. |
| `!gridvault reject <request-id>` | Rejects a request. |
| `!gridvault webhook` | Shows audit webhook status. |
| `!gridvault webhook test` | Sends a test audit embed. |

## Important Configuration Defaults

| Setting | Default | Reason |
|---|---:|---|
| `BackupIntervalMinutes` | `30` | Regular recovery points without constant file writes. |
| `MinimumBlocks` | `25` | Skips tiny throwaway grids. |
| `BackupsPerGrid` | `12` | Retains useful recovery history. |
| `IncludeNpcGrids` | `false` | NPC grids are not stored unless explicitly enabled. |
| `IncludeStaticGrids` | `false` | Bases and static stations are not stored unless explicitly enabled. |
| `EnablePlayerRecoveryRequests` | `true` | Players may request; only admins approve. |
| `EnableAuditWebhook` | `false` | Webhook traffic is opt-in. |

## Discord Audit Embeds

Set `EnableAuditWebhook` to `true` and add a full Discord webhook URL to `AuditWebhookUrl` in the generated configuration. Use a private staff-only channel: embeds can include Steam IDs, grid IDs/names, timestamps, verification results, and approved GPS locations.

With `SendStartupWebhookTest=true`, Gridvault posts one green online test embed when a valid webhook is first configured. Run `!gridvault webhook test` for another test.

## Safety Checklist

1. Test on a development world first.
2. Run `preview` before important restores.
3. Choose an open GPS area for `recoverat`.
4. Keep the backup directory outside the active world save folder.
5. Keep webhook URLs private.
6. Keep more than one external copy of critical server backups.

## Known Scope

Connected mechanical and connector grid grouping is not yet enabled. It will be added only after capture and restore behavior is verified against the current Keen API.

## Support and Use

Use of this release is subject to the included license. Report issues with the Gridvault version, Torch version, Space Engineers version, host OS, command used, and relevant Torch log excerpt. Do not include webhook URLs or private server data in public reports.
