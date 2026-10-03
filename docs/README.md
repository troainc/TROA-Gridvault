# Gridvault+ documentation

Gridvault+ is a server-side Torch plugin for scheduled grid backups and controlled recovery. Players can inspect their own grid history and request help; administrators approve and perform restores.

- Follow [Install](../README.md#install) and preserve the generated `TROAGridVault.cfg`.
- Use the [player and administrator command reference](../README.md#commands).
- Read [Restoring a Grid step by step](../README.md#restoring-a-grid-step-by-step) before using recovery commands.
- Keep the backup directory documented in [Backup Folder Layout](../README.md#backup-folder-layout) in your server backup plan.
- For Discord audits, use the webhook configuration and status commands in the README; the webhook is optional and does not require Monitor+.
- Check [CHANGELOG.md](../CHANGELOG.md) for config and command changes.

Recommended first run: install the current release, start Torch to generate config, review capture filters/retention/storage location, run `!gridvault overview`, then test a backup and restore in a safe environment before relying on production recovery.
