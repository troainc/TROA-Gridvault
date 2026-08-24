# TROA-Gridvault

## Modern Grid Backup and Recovery for Space Engineers Torch Servers

TROA-Gridvault is a no-UI, command-driven Torch plugin that protects Space Engineers grids with scheduled backups, Steam-ID-first storage, safe recovery tools, player recovery requests, and optional Discord audit embeds.

This public repository contains **release packages and documentation only**. Source code, private configuration, server data, and webhook URLs are not included.

## No UI — Deliberately Command Driven

Gridvault does **not** install an in-game screen, terminal block, client mod, desktop application, or web panel. Every action is handled through the generated XML configuration and `!gridvault` commands in the Space Engineers in-game chat. This makes setup consistent for Windows, Linux, and AMP-hosted Torch servers.

- **Players:** `!gridvault mine` and `!gridvault request`.
- **Administrators:** backup, verification, restore, cleanup, and webhook commands under `!gridvault`.
- **Torch:** Gridvault runs server-side as a Torch plugin; no player-side install is required.
- **Discord:** optional staff-only audit embeds use a direct Discord webhook. TROA Discord Monitor is not required.
- **Discord-to-Torch bridges:** if a server already has a secure command bridge, staff can forward supported administrator commands such as `!gridvault recoverat ...`. Gridvault does not create Discord slash commands or mirror player chat.

## Why Use Gridvault

- **Steam-ID-first backups** — player backup folders remain useful after world wipes and Keen identity changes.
- **Grid history catalog** — qualifying player grids are tracked by Steam ID with known names, IDs, last-seen time, and retained-backup status.
- **Readable files** — each backup is stored in a timestamp folder and uses the grid's full name as the SBC filename.
- **Safer recovery** — preview a backup before restoring it, then restore near an admin, at exact GPS coordinates, or at the saved location.
- **Collision protection** — restores use a conservative grid-size safety radius and refuse locations that are occupied.
- **Player requests** — players can view their own backups and ask staff for a restore without receiving admin rights.
- **Audit-ready** — optional Discord embeds track backups, restores, verification, failures, and player requests.
- **Operations-ready** — optional player quotas, categories, missing-grid alerts, pre-cleanup safeguards, pre-wipe reports, and controlled migration tools.
- **Host friendly** — designed for Windows, Linux, and AMP-hosted Torch servers; no desktop UI required.

## Complete Feature List

- **No-UI server plugin:** command/config-driven Torch plugin; no player-side mod, terminal block, desktop app, or web panel.
- **Automatic and manual backups:** scheduled passes, `storeall`, single-grid capture, pre-restart safeguard, and Essentials-friendly `precleanup` protection.
- **Selectable grid coverage:** block minimum, name exclusions, optional NPC grids, and optional static bases/stations.
- **Validated storage:** atomic writes, SBC read-back checks, SHA-256 validation, retention, bounded file writes, readable names, and timestamped folders.
- **Steam-ID-first vaults:** player recovery remains tied to Steam ID through world wipes and Keen identity changes.
- **Historical grid finder:** tracks player grid names after renames, entity IDs, first/last seen time, block count, categories, and retained-backup availability.
- **Player tools:** players can list history, request by name or ID, and tag grids as Ship, Base, Mining, Combat, Other, or None.
- **Safe restoration:** preview and audit backups; restore near an admin, at GPS, or at original coordinates with collision and duplicate protection.
- **Ownership choices:** configure Player, Original, or Neutral ownership after a recovery.
- **Server-owner controls:** optional player storage/count quotas, one-time missing-grid alerts, history-only request alerts, health reports, and live configuration reload.
- **Wipes and migrations:** pre-wipe reports, pre-cleanup safeguards, and controlled per-player export/import folders.
- **Standalone Discord audits:** optional webhook embeds for every major operation with clear colors, fields, timestamps, and GridVault footer branding. TROA Discord Monitor is not required.

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

All Gridvault commands are issued in the **Space Engineers in-game chat** unless a server owner deliberately forwards an administrator command through an existing, secured Torch command bridge.

## Backup Folder Layout

```text
TROAGridVaultBackups/
  Players/<steam-id-64>/<utc-timestamp>/<full-grid-name>.sbc
  Players/<steam-id-64>/GridHistory/<grid-entity-id>.xml
  KeenIdentities/<keen-identity-id>/<utc-timestamp>/<full-grid-name>.sbc
  Unowned/<utc-timestamp>/<full-grid-name>.sbc
  RestoreRequests/
```

- `Players` is the preferred location for player-owned grids.
- `GridHistory` records each qualifying player grid seen by GridVault, including names after renames. It helps players identify lost grids; it is not a substitute for a retained SBC backup.
- `KeenIdentities` is used when a grid has a Keen identity but no resolved Steam owner.
- `Unowned` contains truly ownerless grids.
- Existing older backup folders remain readable and are not moved automatically.

## Commands

### Players

| Command | Use |
|---|---|
| `!gridvault help` | Shows GridVault player and administrator command guidance in game. |
| `!gridvault mine` | Lists historical player grids once each with the latest name, ID, revision count, date, and block count. |
| `!gridvault request <grid-name-or-id> [revision]` | Requests recovery by grid name or ID; quote names containing spaces, such as `!gridvault request "Mining Rover"`. Staff approval is required. |
| `!gridvault category <grid-name-or-id> <Ship|Base|Mining|Combat|Other|None>` | Labels a personal grid-history entry. |

### Server Administrators

| Command | Use |
|---|---|
| `!gridvault help` | Shows command help in game. |
| `!gridvault reload` | Reloads configuration without restarting Torch. |
| `!gridvault overview` | Shows backup queue and settings. |
| `!gridvault storeall` | Backs up qualifying server grids. |
| `!gridvault archive` | Alias for `storeall`. |
| `!gridvault safeguard` | Starts a backup pass before an external restart. |
| `!gridvault precleanup` | Starts a backup pass before an Essentials or other configured cleanup. |
| `!gridvault prewipe [note]` | Creates a pre-wipe report and starts a backup pass. |
| `!gridvault capture <grid-id>` | Backs up one grid immediately. |
| `!gridvault records <steam-id> [grid]` | Lists grid history and revisions. |
| `!gridvault preview <steam-id> <grid-id> [revision]` | Shows backup details and original GPS. |
| `!gridvault audit <steam-id>` | Verifies backup hashes and SBC readability. |
| `!gridvault health` | Shows storage usage, incomplete entries, and pending writes. |
| `!gridvault export <steam-id>` | Copies a player vault into the migration export folder. |
| `!gridvault import <steam-id> <folder-name>` | Imports a staged migration folder from GridVault Imports. |
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
| `EnablePlayerGridCategories` | `true` | Players may label history entries. |
| `MaximumBackupsPerPlayer` | `0` | Optional retained-backup cap; `0` is unlimited. |
| `MaximumPlayerVaultMegabytes` | `0` | Optional player storage cap; `0` is unlimited. |
| `MissingGridAlertMinutes` | `0` | Optional one-time missing-grid alert; `0` disables it. |
| `RestoreOwnershipMode` | `Player` | `Player`, `Original`, or `Neutral` after recovery. |
| `EnableAuditWebhook` | `false` | Webhook traffic is opt-in. |

## Discord Audit Embeds

Set `EnableAuditWebhook` to `true` and add a full Discord webhook URL to `AuditWebhookUrl` in the generated configuration. Use a private staff-only channel: embeds can include Steam IDs, grid IDs/names, timestamps, verification results, and approved GPS locations. GridVault embeds use colored outcome states, structured fields, timestamps, and a consistent audit footer.

With `SendStartupWebhookTest=true`, Gridvault posts one green online test embed when a valid webhook is first configured. Run `!gridvault webhook test` for another test.

## Essentials and Migration

Essentials cleanup is external to GridVault. Configure the same secured command workflow to run `!gridvault precleanup` about ten minutes before cleanup; GridVault then queues a full backup pass and posts an audit event. `MissingGridAlertMinutes` can provide a one-time follow-up alert when a cataloged grid is no longer observed.

For migration, run `!gridvault export <steam-id>` on the source server, copy the created export folder into `Imports/<folder-name>` on the destination vault, then run `!gridvault import <steam-id> <folder-name>`. Review records and previews before restoring.

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
