# Player guide

Gridvault+ is a server-side backup and recovery plugin. You do not install anything on your client. Use the commands in Space Engineers chat with the `!gridvault` prefix.

## See your grid history

Run:

```text
!gridvault mine
```

This lists the player grids Gridvault has observed and indexed, with their latest known name, entity ID, revision count, last-seen information, and block count. History helps identify a grid after it is renamed or disappears. **A history entry does not guarantee that a backup file is still retained.** Ask staff to check available revisions if you need a restore.

## Label a grid

Use a category to make your history easier to search:

```text
!gridvault category <grid-name-or-id> <Ship|Base|Mining|Combat|Other|None>
```

Example:

```text
!gridvault category "Mining Rover" Mining
```

Categories organize your history; they do not change backup scheduling or permissions.

## Ask staff to restore a grid

Send a recovery request:

```text
!gridvault request <grid-name-or-id> [revision]
```

Example:

```text
!gridvault request "Mining Rover"
```

You can include the revision number if staff identified a particular copy. Your request goes to server staff for review. Players cannot approve or deploy their own requests. An administrator will choose a safe location and complete the restore.

## What happens to a restored grid

By default, a restore is assigned to the grid owner. If you are online, the grid is placed in clear space near you. If you are offline and the server has Hangar+, Gridvault can hand the restored grid to your Hangar storage; otherwise, it will deploy near you when you next log in. The server owner controls the restore policy.

Gridvault keeps the backup after a restore. A backup can be restored again later, subject to duplicate-grid and collision protections.

## Need help?

Use `!gridvault help` for in-game help. Give staff the grid name or entity ID, your Steam ID if requested, and the approximate time it went missing. Do not post private server paths or Discord webhook URLs.
