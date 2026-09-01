# v0.3.3 - Quiet Discord Failure Circuit

- Removed repeated Discord webhook failure messages from the live Torch/game-server console.
- Added a quiet circuit breaker that pauses delivery for ten minutes after three consecutive failures.
- Added safe failure count, HTTP status, and pause information to `!gridvault webhook` without exposing the webhook URL.
- Made `!gridvault webhook test` report when the failure circuit is paused.
- A successful delivery resets the consecutive-failure circuit; `!gridvault reload` resets it immediately after configuration is corrected.

# v0.3.2 - Gridvault+ Runtime Branding

- Changed the default player-facing and in-game runtime name to `Gridvault+`.
- Added the owner-configurable `DisplayName` setting for chat replies, runtime notices, reports, log prefixes, GPS labels, and Discord audit embeds.
- Preserved `TROA-Gridvault` and `TROAGridVault` for external repository, package, assembly, configuration-file, namespace, and compatibility identifiers.
- Migrates empty and exact legacy runtime names to `Gridvault+` while preserving custom server branding.
- Updated the example configuration and documentation; the plugin remains fully no-UI.

# v0.3.1 - Player Command Access Hotfix

- Fixed `!gridvault help` so every in-game player can view the player command guidance.
- `!gridvault mine`, `!gridvault request`, and `!gridvault category` remain available to players; administrator actions stay protected.

# v0.3.0 - Vault Operations and Audit Upgrade

- Added optional per-player backup count and vault storage limits.
- Added optional missing-grid alerts, player categories, and history-only request alerts.
- Added Essentials-friendly `precleanup`, pre-wipe reports, and controlled migration export/import folders.
- Added Player, Original, and Neutral restored ownership modes.
- Redesigned Discord audit embeds with color states, fields, timestamps, and GridVault footer branding.

# v0.2.2 - Player Grid History and Friendly Requests

- Added a Steam-ID-backed player grid history catalog under `Players/<steam-id>/GridHistory`.
- Tracks qualifying player grids with entity IDs, known names after renames, first/last observed time, and block count.
- `!gridvault mine` now shows one historical grid entry at a time, including retained-backup status.
- `!gridvault request` now accepts either a grid ID or a grid name; quote names containing spaces.
- Exact name matching is preferred; partial names only work when they identify one grid.
- Qualifying grids remain visible in player history even when the backup write queue is temporarily full.

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
