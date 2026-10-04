# Configuration reference

The complete example is [`TROAGridVault.cfg.example`](../TROAGridVault.cfg.example). Torch generates the active `TROAGridVault.cfg` on first startup. Edit the installed config, save it, then run `!gridvault reload`. Do not publish the active config if it contains webhook URLs or private paths.

| Setting | Example default | Meaning / guidance |
|---|---:|---|
| `DisplayName` | `Gridvault+` | Branding for chat, reports, logs, GPS labels, and audit embeds. |
| `Enabled` | `true` | Master switch for scheduled backup passes. Manual admin commands remain available. |
| `VaultRootPath` | empty | Blank uses the default `TROA-Gridvault-Backups` folder. Otherwise use a durable absolute path. |
| `BackupFolderTimeZoneId` | `Local` | Time zone used in readable backup folder names. Supports aliases such as `Eastern`, `UTC`, or OS zone IDs. |
| `BackupIntervalMinutes` | `30` | Interval between automatic backup passes. |
| `MinimumBlocks` | `25` | Grids smaller than this are skipped by normal capture. |
| `BackupsPerGrid` | `12` | Number of newest revisions to retain per grid. |
| `DailyBackupsPerGrid` | `7` | Reserved for daily retention support; keep the example default unless current release docs say otherwise. |
| `RetainDays` | `30` | Remove backup files older than this retention age. |
| `MaximumPendingBackups` | `8` | Maximum backup writes waiting in memory. |
| `MaximumConcurrentWrites` | `1` | Concurrent file writes; one is the conservative setting. |
| `MaxGridsPerTick` | `4` | Grids captured each simulation tick; lower values spread work over more ticks. |
| `MaxCaptureMillisecondsPerTick` | `8` | Time budget for grid capture per tick. |
| `SkipUnchangedGrids` | `true` | Skip grids whose name and block count did not change since their previous backup. |
| `ForceBackupAfterMinutes` | `1440` | Refresh an unchanged grid after this many minutes; `0` disables forced refresh. |
| `PreferHangarForOfflineRestores` | `true` | Hand an offline player's restore to Hangar+ when installed; otherwise deploy on next login. |
| `RestoreSpawnDistanceMeters` | `60` | Spawn distance from the player for nearby restores. |
| `MaxFindResults` | `50` | Maximum results returned by `!gridvault find`. |
| `IncludeMechanicallyConnectedGrids` | `true` | Planned connected-grid control in the sample; leave as shipped unless current plugin release documents support. |
| `IncludeConnectorConnectedGrids` | `false` | Planned connected-grid control; leave as shipped unless documented as active. |
| `IncludeProjections` | `false` | Planned projection control; leave as shipped unless documented as active. |
| `IncludeStaticGrids` | `false` | Include static bases/stations in normal capture. Enable deliberately. |
| `IncludeNpcGrids` | `false` | Include NPC-owned grids in normal capture. Enable deliberately. |
| `KeepOriginalOwners` | `true` | Compatibility setting related to preserving ownership. Check release notes before changing. |
| `EnableAutomaticCleanup` | `true` | Master for automated cleanup/retention work as described by the current release. |
| `EnablePlayerRecoveryRequests` | `true` | Allows players to request recovery; administrator approval is always required. |
| `EnablePreRestartBackup` | `true` | Allows `!gridvault safeguard` before external restart workflows. |
| `EnablePlayerGridCategories` | `true` | Allows players to label their own grid history. |
| `MaximumBackupsPerPlayer` | `0` | Maximum retained revisions for one player; `0` means unlimited. |
| `MaximumPlayerVaultMegabytes` | `0` | Player storage quota in MB; `0` means unlimited. |
| `MissingGridAlertMinutes` | `0` | One-time alert delay for a cataloged grid not seen; `0` disables. |
| `EnableCleanupGridPreservation` | `true` | Preserve the newest valid backup in the permanent Cleanup Grids area when a player grid disappears. |
| `CleanupGridGraceMinutes` | `10` | Delay before a missing grid is treated as cleaned up/deleted for preservation. |
| `RestoreOwnershipMode` | `Player` | Ownership after recovery: `Player`, `Original`, or `Neutral`. |
| `ExcludedGridNamePatterns` | empty | Grid-name patterns skipped by capture. Add `<string>pattern</string>` elements if using a list. |
| `EnableAuditWebhook` | `false` | Enables the optional audit webhook. |
| `AuditWebhookUrl` | empty | Full private Discord webhook URL for audit events. |
| `SendStartupWebhookTest` | `true` | Sends one startup test embed when the webhook is first configured. |
| `AdminCommandWebhookUrl` | empty | Separate optional staff webhook that logs the actor and full admin command. |

**Version rule:** a sample may include reserved or planned settings not recognized by every released binary. Check the package's README/changelog before relying on any setting labelled planned/reserved. After reload, use `!gridvault overview` and check Torch logs for errors.
