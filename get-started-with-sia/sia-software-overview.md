---
description: A side-by-side guide to the Sia software and the terms used across these docs.
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

# Which Sia software do I need?

There are several pieces of Sia software, each for a different job. Use this page to find the one that matches what you want to do.

| I want to… | Use |
|------------|-----|
| Store and manage files the easy way | The **Sia Storage app** (desktop, mobile) with a [Sia Storage](https://sia.storage) account — 50 GB free |
| Use Sia through an S3-compatible API | [`s3d`](https://github.com/SiaFoundation/s3d), connected to an indexer such as Sia Storage |
| Build my own app | The [Sia Storage SDKs](https://devs.sia.storage) |
| Run the indexer myself instead of using Sia Storage | [`indexd`](../renting/setting-up-indexd/) — requires PostgreSQL |
| Provide storage and earn Siacoin | [`hostd`](../hosting/about-hosting-on-sia.md) |
| Hold and manage Siacoin | [`walletd`](../wallet/wallet-overview.md) |
| Run the older all-in-one renter | [`renterd`](../renting/setting-up-renterd/) — no longer the preferred way to store data |

## How the pieces fit together

To store data on Sia you run a **client** that connects to an **indexer**. The client encrypts your files and moves them to and from storage providers; the indexer manages contracts and keeps your data healthy. By itself, an indexer like Sia Storage doesn't store your files — you need a client to use it. See [About Storing Your Data](../renting/about-renting.md) for more.

### Clients — how you use Sia storage

* **Sia Storage app** — desktop and mobile apps for storing and retrieving files. Point it at an indexer; a Sia Storage account is the easiest option.
* **`s3d`** — a lightweight, S3-compatible gateway. It translates the AWS S3 API to Sia and connects to an indexer such as Sia Storage, so existing S3 tools and applications can use Sia storage.
* **Sia Storage SDKs** — client libraries (Rust, Go, Python, JavaScript) for building your own app. The Sia Storage app and `s3d` are currently the only ready-made clients.

### Indexer — the backend

* **Sia Storage** — a hosted indexer. It manages contracts and keeps your data healthy for you, with 50 GB free and nothing to run. Recommended for most people.
* **`indexd`** — the indexer software, for running the backend yourself instead of using Sia Storage. Requires PostgreSQL.

### Other software

* **`hostd`** — storage-provider software. Stores encrypted data for the network and earns Siacoin.
* **`walletd`** — a standalone wallet for Siacoin and Siafunds, with Ledger support.
* **`renterd`** — the original all-in-one renter (wallet, contracts, and an upload/download UI in one program). Still works, but no longer the preferred way to store data.

## Glossary

* **Renter** — anyone storing data on Sia. The renter forms and pays for storage contracts; today an indexer fills this role on your behalf.
* **Storage provider (host)** — an operator running `hostd` that stores encrypted data and earns Siacoin.
* **Client** — software you run to store and retrieve files, such as the Sia Storage app or `s3d`. A client connects to an indexer.
* **Indexer** — the backend that manages contracts, tracks where data lives, and keeps it healthy. Sia Storage is a hosted indexer; `indexd` is the software for running your own.
* **Contract** — a blockchain-enforced agreement between a renter and a storage provider covering how much data to store, for how long, and at what price.
* **Object** — the application-level view of a stored file: its data, metadata, and storage layout under a single content-derived ID.
* **Slab** — a unit of an object's data that is erasure-coded into shards.
* **Shard** — one erasure-coded, encrypted piece of a slab, stored by a single provider.
* **Erasure coding** — a method of splitting data into redundant pieces so the original can be rebuilt from a subset of them.
* **Siacoin (SC)** — the network's utility token, used to pay for storage.
* **Siafund** — a separate token that receives a fee from storage contracts.
* **Recovery phrase (seed)** — the secret words that control a wallet and let you recover it.
