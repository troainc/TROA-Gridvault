# Gridvault+ Roadmap

Gridvault+ owns grid backup, history, recovery, and its audit webhooks. This roadmap describes product priorities, not release commitments.

## Priorities

1. **Release integrity:** install packages only from the published GitHub Releases page. Confirm package version and checksum against release metadata before deployment; local or untracked ZIPs are not release proof.
2. **Restore preflight:** estimate affected grids and storage, check disk headroom, report retention impact, and show collision risks before an owner confirms a restore.
3. **Recovery validation:** add a dry-run validation of backup readability, hashes, SBC data, and target clearance before paste or handoff.
4. **Operational recovery:** test interruption/restart recovery, Hangar handoff, pending restore on login, and catalog reconstruction without overwriting valid backup files.
5. **Scale visibility:** expose bounded storage growth, quota, retention, and queue summaries for large vaults.

Gridvault+ remains the sole owner of its vault and recovery history. Cleaner+ may request preservation through the supported integration API but must not take over the vault.
