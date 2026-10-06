# Gridvault+ — backup and recovery guide

Gridvault+ is a Torch-side vault for Space Engineers grid snapshots and recovery. It owns backup files, grid history, restore requests, restore operations, and its optional audit webhooks. Players need no client mod. Monitor+ is not required. Start from the [owner setup guide](SERVER-OWNER-SETUP.md), then read [configuration](CONFIGURATION.md), [commands](COMMANDS.md), [recovery](RECOVERY.md), [migration](MIGRATION.md), and [troubleshooting](TROUBLESHOOTING.md).

## What is saved

Gridvault stores versioned grid snapshots and metadata so operators can inspect grid history and choose a suitable recovery point. Configure storage root, retention/cleanup limits, snapshot behavior, and available integrations before production use. Preserve the whole vault data directory in backups. A snapshot is not automatically a guarantee that every external world dependency or mod definition can be restored; test with representative grids and the same server mod set.

## Player workflow

Players can inspect their eligible grid history, label/identify grids, and request staff recovery where the server enables these commands. The player guide explains what information to provide. Players should not repeatedly issue restore requests while a previous request is pending. A request does not immediately replace a live grid; staff review and authorization rules apply.

## Administrator workflow

Install the release in Torch and verify storage is writable. Perform a manual/automatic snapshot as configured, inspect history, and use a preview or recovery workflow to confirm the selected snapshot, target, ownership, and spawn/placement context before restoring. Process player requests from the queue, approve or deny with a clear reason, and inspect the result in logs. Use the migration guide when importing another vault; validate imported counts and sample restores before retiring the old backup set.

Cleaner+ can request a pre-delete backup through the supported bridge; Gridvault remains the owner of that snapshot and its recovery. Hangar+ integration, where enabled in both installed builds, is likewise an integration and does not transfer vault ownership. Keep each plugin's webhook and permissions scoped to its own work.

## Safety and operations

Take a separate copy of the vault before a major restore, migration, retention change, or plugin update. Avoid editing/deleting vault files while Torch is running. Keep credentials out of public config samples. Follow the exact current release documentation because command availability and migration support are versioned. In an incident, preserve logs and vault files first, then use the troubleshooting guide before attempting manual recovery.
