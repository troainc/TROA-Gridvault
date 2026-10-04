# Troubleshooting

## Plugin or command is missing

Confirm the current `TROAGridVault-v*.zip` is installed once in Torch's `Plugins` folder and check startup logs for a load or command-registration error. Commands use `!gridvault` in Space Engineers chat. Admin-only commands require Torch administrator permission. Gridvault does not expose its own Discord command bot.

## No backup appears

Check `!gridvault overview` and `!gridvault health`, then review `Enabled`, `VaultRootPath`, `MinimumBlocks`, `IncludeNpcGrids`, `IncludeStaticGrids`, and `ExcludedGridNamePatterns`. Unchanged grids may be skipped when `SkipUnchangedGrids` is on; a periodic refresh is controlled by `ForceBackupAfterMinutes`. Check free disk space and Torch write permissions. Run `!gridvault save` while looking at a qualifying grid, then inspect history/records.

## History exists but backup is unavailable

Grid history tracks observed names and IDs and is not itself a retained `.sbc` backup. Retention, quota settings, excluded grid criteria, or a previous failed capture may explain the missing file. Check `!gridvault list`, `!gridvault preview`, `!gridvault audit`, and `!gridvault health`; review the server log for capture/write errors.

## Restore is refused or lands somewhere unexpected

Preview the selected revision and verify the owner/grid IDs. Gridvault avoids duplicate entity IDs and blocked placement. Choose a clear space or use the documented original-position/force options only after assessing collision risk. Check `RestoreOwnershipMode`, `RestoreSpawnDistanceMeters`, `PreferHangarForOfflineRestores`, and whether Hangar+ is installed. Do not repeatedly force a blocked restore.

## Player did not receive an offline restore

If `PreferHangarForOfflineRestores` is enabled and Hangar+ is installed, check the player's Hangar after their next login. Otherwise Gridvault holds the restore for next-login deployment. Review Torch logs and the restore audit entry before retrying to avoid duplicates.

## Config reload reports an error

Validate XML nesting and spelling against [`TROAGridVault.cfg.example`](../TROAGridVault.cfg.example). Save the active config and run `!gridvault reload`; review Torch logs and confirm with `!gridvault overview`. Do not assume malformed or unsupported settings were accepted. Config examples can document reserved fields not active in every release.

## Discord audit messages stopped

Run `!gridvault webhook` to check a safe status, failure count, HTTP status, and pause state. Verify the full webhook URL privately, then run `!gridvault reload` and `!gridvault webhook test`. After three consecutive Discord failures, Gridvault pauses retries for ten minutes. Rotate any webhook URL posted publicly. Monitor+ is not involved in this direct webhook delivery.

## Backups slow the server or fill disk

Lower `MaxGridsPerTick`, `MaxCaptureMillisecondsPerTick`, and `MaximumConcurrentWrites`; increase `BackupIntervalMinutes`; enable `SkipUnchangedGrids`; adjust retention and quotas. Change one setting at a time and inspect `!gridvault overview` pass duration and `!gridvault health` storage usage.

## Get support

Report the Gridvault package version, Torch/Space Engineers versions, host OS, command, exact error, and relevant sanitized log lines. Do not include webhook URLs, player private data, or full server paths in public reports.
