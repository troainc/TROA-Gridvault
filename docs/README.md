# Gridvault+ Documentation

This handbook explains Gridvault+ for Space Engineers Torch servers. Gridvault+ runs on the server; players do not install a mod or use a separate app. Commands are entered in game chat. A server owner may optionally forward administrator commands through a secured command bridge.

## Pick a guide

- [Player guide](PLAYER-GUIDE.md) — find your grid history, label grids, and request a recovery.
- [Server owner setup](SERVER-OWNER-SETUP.md) — install, configure backups, validate storage, and prepare safe recovery.
- [Configuration reference](CONFIGURATION.md) — every setting in the public config example, with defaults and setup advice.
- [Command reference](COMMANDS.md) — player and administrator command syntax.
- [Recovery guide](RECOVERY.md) — search, preview, restore, and handle player requests safely.
- [Migration guide](MIGRATION.md) — move backups from ALE GridBackup or another Gridvault server.
- [Troubleshooting](TROUBLESHOOTING.md) — diagnose missing backups, restore failures, configuration, and Discord delivery.

The complete credential-free XML example is [`TROAGridVault.cfg.example`](../TROAGridVault.cfg.example). The root [README](../README.md) is the feature overview; this handbook is the how-to documentation. Check [CHANGELOG](../CHANGELOG.md) and the [GitHub Releases](https://github.com/troainc/TROA-Gridvault/releases) page for version-specific changes and packages.

## What Gridvault owns

Gridvault+ owns grid backup files, grid history, recovery requests, restores, and its optional audit webhooks. Discord Monitor+ is not required and does not own or relay Gridvault's events. Another plugin may call Gridvault's documented integration API to request a backup before cleanup, but Gridvault retains its own vault and recovery commands.
