---
description: Back up, move, and recover indexd
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Backing up and recovering indexd

PostgreSQL contains the operational state of an `indexd` installation. A tested database backup is the primary way to recover or move the service without losing accounts, contracts, settings, and maintenance state.

{% hint style="danger" %}
**The `indexd` recovery phrase is not a backup of the indexer.** It can recover the on-chain wallet balance after a blockchain rescan, but it cannot recreate the object index, contracts, or application accounts.
{% endhint %}

## Back up PostgreSQL

Use normal production PostgreSQL practices:

* Run scheduled automated backups; use WAL archiving and point-in-time recovery for larger or critical deployments.
* Keep backups outside the `indexd` machine and storage volume.
* Test restores regularly and monitor backup failures, database health, disk space, and WAL retention.
* Use a dedicated database and role. Use verified TLS when connecting over an untrusted network.
* Back up `indexd.yml` and the data directory, and store the wallet recovery phrase separately.

For Docker Compose, use PostgreSQL-aware tooling such as `pg_dump`, a managed-service snapshot, or a physical base backup. Copying a live `postgres` volume is not an application-consistent backup.

## Do not share a database

Only one full `indexd` daemon may use a PostgreSQL database at a time. Multiple daemons are not supported or safe: `indexd` has no database-wide leader election, and each instance runs its own consensus, wallet, contract, and maintenance services.

Use active/passive failover and ensure the old process is stopped before starting its replacement. The `indexd remote` migration worker is different: it has no database connection and only performs work assigned by the primary node.

## What can be recovered

| Surviving state | What it can recover |
| --- | --- |
| PostgreSQL | Server-side state, including application accounts and connect keys, contracts, object and slab records, sector locations, settings, and wallet scan state. |
| `indexd` wallet recovery phrase | The wallet identity and on-chain balance after a rescan. It does not recover the index. |
| Application recovery phrase and a surviving indexer | After normal reauthorization, the app can rebuild its local state from the object metadata it stored on that indexer. |
| A complete application metadata cache | The app can pin its objects to a replacement indexer without moving the object payload. The cache must contain the object keys and complete slab layouts, not only object IDs. |

If both the application cache and the indexer's PostgreSQL state are lost, neither recovery phrase can reconstruct the missing object metadata.

## Move or restore indexd

### Restore from a database backup

1. Stop `indexd` before the final backup.
2. Back up PostgreSQL and copy the `indexd` data directory, including `indexd.yml` and `consensus.db`.
3. Restore both on the replacement server, configure the same wallet recovery phrase, and initially use the same `indexd` version.
4. Start exactly one `indexd` instance and wait for consensus and wallet synchronization.
5. Verify the wallet balance, contracts, application accounts, connect keys, and object health before switching applications or upgrading.

If the public application API URL stays the same, existing applications can continue using their saved credentials after traffic moves to the replacement.

### Recover from an application's local cache

This is a last-resort fallback when PostgreSQL is permanently lost, not a substitute for database backups:

1. Preserve the application's local metadata cache. Do not sign out, clear its storage, or reinstall it.
2. Set up, synchronize, and fund a replacement `indexd` so it can form contracts.
3. Create a connect key on the replacement and connect the application normally. The lost indexer is not required.
4. Have the application pin its cached object and slab metadata to the replacement. The replacement can pin the sectors already held by storage providers under its contracts; the object payload does not need to be uploaded again.
5. Wait for pinning and contract maintenance to finish, then verify the object list, health, and test downloads before deleting any recovery state.

Moving even a large metadata catalog is far cheaper than downloading and re-uploading. Start promptly after a loss, because the old indexer is no longer renewing contracts or repairing redundancy. Only objects present in the local cache can be recovered this way.
