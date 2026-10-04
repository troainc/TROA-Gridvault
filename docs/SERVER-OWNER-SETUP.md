# Server owner setup

Gridvault+ is a command- and configuration-driven Torch plugin for Space Engineers. It does not install a client mod, terminal block, or web panel.

## 1. Install

1. Download the newest `TROAGridVault-v*.zip` asset from [GitHub Releases](https://github.com/troainc/TROA-Gridvault/releases).
2. Stop Torch and install the release ZIP using your Torch host's normal plugin process. Remove older duplicate Gridvault packages so Torch loads only one copy.
3. Start Torch. Gridvault creates `TROAGridVault.cfg` and the default `TROA-Gridvault-Backups` directory.
4. Confirm the plugin loaded in the Torch log. In game as an admin, run `!gridvault overview` and `!gridvault health`.

## 2. Choose and protect the vault location

Set `VaultRootPath` to an absolute durable path if you do not want to use the default plugin folder. Keep the vault outside the active world-save directory when practical. Confirm the Torch process can create folders and write files there, and that the disk has sufficient free space.

Back up the vault independently of the world. Player data is grouped under `Players/<steam-id-64>/`; additional folders hold NPC, unowned, cleanup-preservation, Keen-identity, history, and recovery-request data. See the root README's Backup Folder Layout. Do not rename or manually edit files while Torch is running.

## 3. Set a backup policy

Review these before relying on the plugin:

- `BackupIntervalMinutes`, `MinimumBlocks`, `BackupsPerGrid`, and `RetainDays` set scheduled capture and retention.
- `SkipUnchangedGrids` and `ForceBackupAfterMinutes` reduce repeat writes while still allowing a periodic safety refresh.
- `MaxGridsPerTick` and `MaxCaptureMillisecondsPerTick` bound game-thread capture work. Lower limits spread capture across more ticks.
- `IncludeNpcGrids` and `IncludeStaticGrids` are disabled by default. Enable only the grid classes you intend to preserve.
- `ExcludedGridNamePatterns` skips matching grid names.
- Player quotas are unlimited when their setting is `0`.
- `EnableAutomaticCleanup` and `EnableCleanupGridPreservation` control cleanup-related behavior. Read the matching config descriptions and README before changing them.

Use `!gridvault overview` to inspect active settings and queue state. Start with conservative coverage and retention; validate disk usage and capture duration before increasing scope.

## 4. Validate a backup

1. Start in a test world or during a safe maintenance window.
2. Run `!gridvault save` while looking directly at a suitable test grid, or `!gridvault storeall` for a qualifying pass.
3. Run `!gridvault records <steam-id>` and `!gridvault preview <steam-id> <grid-id>` to confirm a revision exists.
4. Run `!gridvault audit <steam-id>` to verify file hashes and SBC readability. Audit runs in the background.
5. Test a restore in a clear, non-production location before relying on backups for an incident.

A normal backup pass captures qualifying grids. `!gridvault backupworld confirm` deliberately overrides normal filters and quotas for that pass; treat it as an exceptional operation and review the confirmation warning before using it.

## 5. Configure optional Discord auditing

Discord audit embeds are disabled by default. To enable them, set `EnableAuditWebhook` to `true`, paste the full webhook URL into `AuditWebhookUrl`, save the private config, and run `!gridvault reload`. Then run `!gridvault webhook` and `!gridvault webhook test`.

Audit embeds may include Steam IDs, grid identifiers, verification results, and approved GPS locations. Use a private staff channel. `AdminCommandWebhookUrl` is a separate optional URL that records administrative commands. Keep both URLs private and never publish the live config. If a URL leaks, revoke it in Discord and replace it.

Monitor+ is not required for Gridvault's webhook. Gridvault owns its own audit delivery and failure handling.

## 6. Prepare operations and recovery

Give staff the [command reference](COMMANDS.md) and [recovery guide](RECOVERY.md). If another server tool restarts Torch, configure its secured workflow to run `!gridvault safeguard` before the restart. Before cleanup, use `!gridvault precleanup`; before a wipe, use `!gridvault prewipe [note]` and verify the resulting backup/report.

After any config edit, run `!gridvault reload`. Check the log and `!gridvault overview`; do not assume an invalid edit was applied. Keep at least one copy of the vault on separate storage.
