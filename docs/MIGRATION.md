# Migration guide

Gridvault provides two distinct migration paths. Back up source and destination data before starting. Both workflows copy data; do not delete the source backups until you have verified the imported records and tested a restore.

## From ALE GridBackup

The separate `GridBackupToGridVaultMigrator` utility copies compatible SBC files into Gridvault's normal vault layout and writes a migration report. It does not change or delete the legacy source.

1. Stop Torch or run the migration against a stable copy of the source backup directory.
2. Extract/run the migrator outside Torch's `Plugins` directory.
3. Run a dry run and inspect the report:

```powershell
.\GridBackupToGridVaultMigrator.exe --source "D:\Server\GridBackups" --target "D:\Server\TROA-Gridvault-Backups" --identity-map ".\identity-map.csv" --dry-run
```

4. If the legacy folders use Steam IDs, the tool can map owners directly. If they use Keen identity IDs, prepare the CSV mapping as `legacy-identity,steam-id` using `identity-map.example.csv`.
5. Run again without `--dry-run` only after reviewing the dry-run results. Unmapped identities are skipped by default to avoid assigning data to the wrong player. Use `--include-unmapped` only when intentionally importing to the staff-review `KeenIdentities` area.
6. Start Torch and validate with `!gridvault records <steam-id>` and `!gridvault audit <steam-id>`. Preview and test a restore before retiring the old vault.

The repository may include a prebuilt migrator ZIP. Confirm its release and checksum from the repository before use. The utility's own usage/help output is authoritative for option names supported by that exact version.

## Gridvault server-to-server transfer

1. On the source server, run `!gridvault export <steam-id>`.
2. Copy the resulting export directory into the destination vault's `Imports/<folder-name>` directory.
3. On the destination, run `!gridvault import <steam-id> <folder-name>`.
4. Verify `!gridvault records <steam-id>`, inspect revisions with `!gridvault preview`, and run `!gridvault audit <steam-id>`.
5. Test a restore before deleting source data.

Keep Steam IDs exact. Never import a player's folder under another player's Steam ID. Retain the generated CSV/report with the migration records.
