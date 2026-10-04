# Recovery guide

A Gridvault restore copies a saved grid into the live world. It does not consume the backup. Administrators should perform recovery; players can only submit requests for staff review.

## Before restoring

1. Identify the owner and grid by entity ID when possible. `!gridvault find <name-or-id>` searches vaults; `!gridvault list <player-or-steamid>` lists an owner's history.
2. List revisions with `!gridvault list <player> <grid>`. Revision `1` is newest.
3. Inspect the intended copy using `!gridvault preview <steam-id> <grid-id> [revision]`.
4. Verify the file with `!gridvault audit <steam-id>` if the backup's integrity is uncertain.
5. Choose an area with enough clear space. Check for a live grid with the same entity ID; Gridvault prevents duplicate deployment.

## Restore to the owner

```text
!gridvault restore <player-or-steamid> <grid> [revision]
```

The default policy assigns the grid to its player owner. An online owner receives it in clear space nearby. An offline owner is handed the grid through Hangar+ when available; otherwise Gridvault holds it for deployment when that owner next joins.

Faction grids can be restored with:

```text
!gridvault restore faction <tag> <grid> [revision]
```

## Restore near staff or at coordinates

To restore near the in-game administrator:

```text
!gridvault recover <steam-id> <grid-id> [revision]
```

To deploy at a specific GPS position:

```text
!gridvault recoverat <steam-id> <grid-id> <x> <y> <z> [revision]
```

To use the original saved position when safe:

```text
!gridvault recoverorigin <steam-id> <grid-id> [revision]
```

The owner-oriented `restore` command supports optional `keepOriginalPos` and `force` flags. `keepOriginalPos=true` requests the saved location. `force=true` bypasses a potentially-blocked warning and can cause overlap; only use it after checking the location and with explicit staff intent. If placement is unsafe, choose another location rather than forcing it.

## Approve a player request

1. Review requests with `!gridvault requests`.
2. Check the player's grid history and the requested grid/revision with `find`, `records`, `list`, and `preview`.
3. Approve at a suitable location with `!gridvault approve <request-id> <x> <y> <z>`.
4. Or deny it with `!gridvault reject <request-id>`.

Tell the player when the restore is complete. Do not promise a restore until you have confirmed a retained backup exists.

## Safety and verification

- Restore does not delete its source backup; retain a separate external copy of important vault data.
- A collision/duplicate check can refuse placement. Resolve the conflicting live grid or choose a safe location.
- Never edit or move `.sbc` files while Torch is running.
- After a restore, confirm the player, grid ownership mode, location, and audit record.
- For an unavailable revision, check retention, quotas, disk health, and `!gridvault health`; history by itself is not a backup.
