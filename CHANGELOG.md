# v0.5.1 - Consolidated Backup Audit Embed

- Removed the per-grid "Grid backup saved" Discord embed that posted once for every backed-up grid, which flooded the audit channel during a pass.
- Each backup pass now posts a single "Grid backup pass complete" summary embed (captured, unchanged, filtered, scanned, duration, and slowest grid).
- The summary embed is sent only when a pass actually captures grids or hits failures, so quiet all-unchanged passes never touch the webhook.
- Removed the redundant per-pass "started" embed; the in-game command reply still confirms a pass has begun.
- Backup failures, restores, verification, missing-grid alerts, cleanup preservation, recovery requests, and pre-wipe/pre-cleanup events still post their own embeds.

# v0.5.0 - Non-Blocking Backups and Change-Aware Vault

- Fixed the server freeze during backup passes: grid capture no longer runs on the simulation thread in one blocking call.
- Backup passes now capture grids a few per tick on the game thread (bounded by `MaxGridsPerTick` and `MaxCaptureMillisecondsPerTick`) and perform all disk work on a background worker.
- Moved player-history writes, quota checks, retention cleanup, and missing-grid detection off the simulation thread.
- Added `SkipUnchangedGrids` (default true): grids whose block count and name are unchanged since their last backup are skipped, greatly reducing server impact and storage.
- Added `ForceBackupAfterMinutes` (default 1440) so unchanged grids still receive a periodic safety refresh.
- Added per-pass throttles `MaxGridsPerTick` (default 4) and `MaxCaptureMillisecondsPerTick` (default 8).
- Retention now builds one cached metadata index per owner per pass instead of rescanning the entire owner folder on every write, removing quadratic slowdown as the vault grows.
- Added end-of-pass telemetry: `!gridvault overview` reports the last pass (captured/unchanged/filtered/scanned, duration, slowest grid), a completion embed is sent to the audit webhook, and slow single grids are logged by name.
- Manual `!gridvault storeall`, `safeguard`, `precleanup`, `prewipe`, `backupworld`, and `capture` now schedule their work on the game thread instead of running heavy serialization on the command thread, and report that the pass has started.
- Fixed a latent bug where a paused audit webhook could also suppress backup file writes; backups now always run regardless of webhook state.
- Configuration reloads now wait for an in-progress pass, not just pending writes.

# v0.4.3 - Consistent Backup Folder Branding

- Renamed the default vault folder from `TROAGridVaultBackups` to `TROA-Gridvault-Backups`.
- Added a one-time atomic legacy-folder rename when the new folder does not exist.
- If the legacy rename cannot complete, GridVault safely continues using the existing folder rather than orphaning backups.
- Custom `VaultRootPath` values are never renamed or changed.

# v0.4.2 - Configurable Backup Folder Timezone

- Added `<BackupFolderTimeZoneId>Local</BackupFolderTimeZoneId>` to generated and example configurations.
- Backup and Cleanup Grids folder names now use the configured timezone instead of UTC.
- Supports `Local`, `UTC`, Pacific, Mountain, Central, Eastern, Atlantic, Alaska, and Hawaii aliases, plus operating-system timezone IDs.
- Portable regional aliases resolve both Windows and Linux timezone identifiers and automatically follow daylight-saving time.
- Stored metadata and Discord timestamps remain UTC for reliable auditing; only human-readable folder names change.

# v0.4.1 - Discord Payload and Console Silence Hotfix

- Made Discord audit payloads ASCII-safe JSON while retaining full Unicode text through escaped code points.
- Added explicit UTF-8 request encoding and charset metadata.
- Rechecks the quiet failure circuit inside queued webhook work so already-queued events stop after the circuit opens.
- Confirmed webhook failures remain available only through `!gridvault webhook`; repeated HTTP errors are not written to the live Torch console.
- A full Torch restart is required after replacing the plugin package so the old loaded assembly cannot continue logging failures.

# v0.4.0 - Full-World and Cleanup Protection

- Added administrator-only `!gridvault backupworld confirm` with an explicit warning and confirmation requirement.
- The confirmed pass captures every live grid, including player, NPC, static, tiny, excluded-name, unowned, and over-quota grids, without changing saved configuration.
- Added a dedicated `NPC/<keen-identity-id>` storage category.
- Flattened new timestamp `Grids` folders so named SBC and metadata files are listed directly without another folder per grid.
- Added permanent `Cleanup Grids/Players/<steam-id>/<timestamp>/Grids` safety archives for previously observed player grids that disappear.
- Added configurable cleanup preservation and grace-period settings, enabled by default with a ten-minute delay.
- Cleanup safety copies participate in player history, recovery requests, previews, verification, and administrator restores when normal retained revisions are no longer available.
- Existing legacy and v0.3.x backup layouts remain readable and are not moved automatically.

# v0.3.4 - Readable Grouped Backup Layout

- Changed new player backup paths to `Players/<steam-id>/<MMDDYYYY-HHMMSS>/Grids`.
- Groups grids captured during the same second into one readable backup set instead of adding a top-level timestamp folder for every grid.
- Stores each grid in a clearly named `<full-grid-name>-<grid-entity-id>` folder to prevent duplicate-name collisions.
- Updated retention cleanup for grouped backup sets while preserving support for all existing legacy backup folders.
- Existing backups are not moved, renamed, or deleted during the upgrade.

# v0.3.3 - Quiet Discord Failure Circuit

- Removed repeated Discord webhook failure messages from the live Torch/server console.
- Added a quiet circuit breaker that pauses delivery for ten minutes after three consecutive failures.
- Added safe failure count, HTTP status, and pause information to `!gridvault webhook` without exposing the webhook URL.
- Made `!gridvault webhook test` report when the failure circuit is paused.
- A successful delivery resets the consecutive-failure circuit; `!gridvault reload` resets it immediately after configuration is corrected.
- Updated the local build script to use temporary compilation storage and place the single approved package directly in `releases/`, preventing duplicate `bin` and singular `release` folders.

# v0.3.2 - Gridvault+ Runtime Branding

- Changed the default player-facing and in-game runtime name to `Gridvault+`.
- Added the owner-configurable `DisplayName` setting for chat replies, runtime notices, reports, log prefixes, GPS labels, and Discord audit embeds.
- Preserved `TROA-Gridvault` and `TROAGridVault` for external repository, package, assembly, configuration-file, namespace, and compatibility identifiers.
- Migrates empty and exact legacy runtime names to `Gridvault+` while preserving custom server branding.
- Updated the example configuration and documentation; the plugin remains fully no-UI.

# v0.3.1 - Player Command Access Hotfix

- Fixed `!gridvault help` so every in-game player can view the player command guidance.
- Confirmed `!gridvault mine`, `!gridvault request`, and `!gridvault category` remain player commands; administrator actions remain protected.

# v0.3.0 - Vault Operations and Audit Upgrade

- Added player backup-count and vault-size limits, both disabled by default.
- Added optional missing-grid audit alerts after a configurable last-seen timeout.
- Added player grid categories: Ship, Base, Mining, Combat, Other, and None.
- Added history-only recovery-request alerts when a player identifies a lost grid without a retained SBC backup.
- Added `precleanup` for Essentials or other cleanup schedules to trigger GridVault before deletion work begins.
- Added `prewipe` reports with player-folder and retained-backup counts plus a backup safeguard pass.
- Added controlled player-vault export/import folders for server migration workflows.
- Added configurable restored ownership modes: Player, Original, and Neutral.
- Redesigned Discord audit embeds with operation labels, color states, structured fields, timestamps, and a consistent footer.

# v0.2.2 - Player Grid History and Friendly Requests

- Added a Steam-ID-backed player grid history catalog under `Players/<steam-id>/GridHistory`.
- Tracks qualifying player grids with their entity ID, known names after renames, first/last observed time, and last known block count.
- Updated `!gridvault mine` to show one historical grid entry at a time with its name, ID, revision count, last-seen time, block count, and whether a retained backup is recoverable.
- Updated `!gridvault request` to accept either a grid ID or a grid name; names containing spaces can be quoted.
- Uses safe exact-name matching first, then accepts a partial name only when it identifies exactly one historical grid.
- Records a qualifying player grid in history even if the backup write queue is temporarily full.

# v0.2.1 - Storage and Configuration Cleanup

- Changed new backup folders to the clean `Players/<steam-id>/<timestamp>` layout.
- Stores new grid SBC files using the grid's full display name instead of `grid.sbc`.
- Clearly separates new `KeenIdentities` and `Unowned` backups; existing backup folders remain untouched and readable.
- Added separate static-base and NPC backup controls, both disabled by default.
- Added a one-time startup Discord webhook test when a valid audit webhook is configured.
- Rebuilt generated configuration files with explicit opening/closing tags and an in-file tip for every setting.
- Updated public-facing product display name to `TROA-Gridvault`.

# v0.2.0 - Recovery Operations Build

- Added configurable Discord audit embeds for backup passes, saved backups, restore activity, verification results, failures, and player recovery requests.
- Added backup previews with original GPS, backup age, block count, owner Steam ID, and saved restore safety radius.
- Added conservative full-grid restore collision checks using the saved grid bounding radius.
- Added `recoverat` for Discord/Torch GPS restores and `recoverorigin` for safe original-location restores.
- Added player self-service backup listing and administrator-approved recovery requests.
- Added backup health reporting, pre-restart safeguard command, excluded grid-name patterns, and live configuration reload support.

# v0.1.0 - First Operational Build

- Created a clean `TROA GridVault` project with no legacy ALE source, UI, or dependencies.
- Added cross-platform path handling, XML configuration, and native administrator commands.
- Added manual and scheduled backup passes for qualifying server grids.
- Added Steam-ID-first folders, XML metadata, SHA-256 hashes, atomic backup publication, retention, and a bounded persistence queue.
- Added list, verification, manual-save, and restore-near-administrator commands.
- Defined the next-stage architecture for connected-grid grouping, richer restore previews, audit adapters, quotas, and player recovery requests.
