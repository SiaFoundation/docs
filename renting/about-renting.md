---
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

# About Storing Your Data

Storing data on Sia means uploading your files to independent operators around the world who have made their disk space available, called **storage providers** (or **hosts**). Your data is encrypted and split into redundant pieces on your own machine before it ever leaves it, then spread across many unrelated storage providers so that no single operator — or outage — can read it or take it offline.

Coordinating all of that (finding providers, forming contracts, placing data, and repairing it over time) is handled for you by the rest of the Sia storage stack, described below.

## How storage works on Sia

Modern Sia storage is built from a few distinct pieces, each with a single job. This is the preferred approach for new projects; the older all-in-one `renterd` renter still works, but it is no longer the recommended starting point.

* **Storage providers (`hostd`)** — the nodes that actually store data. They run Sia's hosting software, contribute disk space and bandwidth, and earn Siacoin (SC) by storing encrypted **shards** and proving over time that the data is still available. They never see filenames, object IDs, or anything about the data they hold.

* **Indexers (`indexd`) — contract management.** An indexer sits between applications and storage providers. It forms and maintains the **storage contracts** with providers, tracks where each object's shards live, monitors their health, and repairs data in the background when redundancy drops. It also enforces a simple access model so multiple apps can share one indexer safely. An indexer only ever sees encrypted metadata and the storage layout — never your plaintext data. This is the "renter" role in the new architecture.

* **SDKs — data storage and retrieval.** The [Sia Storage SDKs](https://devs.sia.storage) (available for Rust, Go, Python, and JavaScript) run inside your application. They encrypt your data and metadata, [erasure-code](https://devs.sia.storage/docs/core-concepts/erasure-coding) it into redundant shards, and upload or download those shards **directly** to and from storage providers. Encryption keys stay with you; neither the indexer nor the providers can read your data.

* **Apps — built on the SDKs.** Applications use an SDK to talk to an indexer and storage providers. The indexer deliberately stays narrow (objects, metadata, health, access), so anything higher-level — filenames, folders, search, sharing, version history — is built at the app layer on top of the SDK.

In short: your **app** uses an **SDK** to encrypt and move data to and from **storage providers**, while an **indexer** manages the contracts and keeps that data healthy.

{% hint style="success" %}
**You don't have to run any of this yourself.** [Sia Storage](https://sia.storage) is a hosted indexer and app that gives you **50 GB free** with nothing to install or maintain. Run your own [`indexd`](setting-up-indexd/) only if you want to control the indexer infrastructure yourself.
{% endhint %}

## Storing and retrieving data with the SDKs

Applications never deal with storage providers by hand. Instead they use a **Sia Storage SDK** — a client library that handles encryption, redundancy, and transfer, and coordinates with an indexer on your behalf. SDKs are available for Rust, Go, Python, and JavaScript:

{% tabs %}
{% tab title="Rust" %}
```sh
cargo add sia_storage
```
{% endtab %}

{% tab title="Go" %}
```sh
go get go.sia.tech/siastorage@latest
```
{% endtab %}

{% tab title="Python" %}
```sh
pip install sia-storage
```
{% endtab %}

{% tab title="JavaScript" %}
```sh
npm install @siafoundation/sia-storage
```
{% endtab %}
{% endtabs %}

Everything that touches your data happens locally, inside the SDK:

* **On upload**, the SDK encrypts your file and its metadata, [erasure-codes](https://devs.sia.storage/docs/core-concepts/erasure-coding) the data into many redundant shards, and uploads those encrypted shards directly to storage providers using provider information already loaded into the SDK. The upload returns an object containing the keys and slab layout; the application then *pins* that object to the indexer so it becomes listable and can be repaired over time.
* **On download**, the application passes an object to the SDK. The SDK uses that object's encryption key and slab layout to fetch enough shards from storage providers, verify their integrity, and decrypt the data locally. If the object is stored locally and the SDK has provider connection information, the application can download it while `indexd` is offline.

Data is addressed by a content-derived **object ID** rather than a file path, and objects are immutable — changing the data produces a new object. Object metadata is opaque, application-defined, and encrypted, so the indexer stores it but can't read it. Because every encryption key stays inside your app, neither the indexer nor the storage providers can ever see your data, your metadata, or even your filenames.

For complete upload, download, and object-management examples in each language, see the [Quickstart](https://devs.sia.storage/docs/quickstart) in the Sia Developer Portal.

## Building apps

In the Sia ecosystem, an **app** is the cryptographic identity of software acting on a user's behalf — not a user account, a wallet, or a storage provider. That identity is what lets a user grant a piece of software access to their data, keep each app's data isolated, and revoke that access later.

An app's identity is built from two parts:

* **App ID** — a 32-byte identifier you (the developer) choose once and ship with your software. It's the same across every install of your app, and because it's an input to key derivation, it must never change after release.
* **App Key** — a per-user signing key derived from the user's **recovery phrase**, your App ID, and a secret issued by the indexer during approval. It's unique to each (user, app, indexer approval), stored securely by your app, and used to sign and authorize every request to the indexer. The recovery phrase itself is never stored or transmitted by the app — only the derived key is kept.

Because the App Key is derived from the recovery phrase, App ID, and indexer-issued secret, two apps from the same user produce different keys and **cannot see or modify each other's data**. This sandboxing is structural — enforced by cryptography, not by server-side rules. Before an app can act for a user it must be explicitly approved once, and approval can be revoked at any time, immediately cutting off that app's access.

Indexers deliberately stay narrow: they track objects, metadata, health, and access, and nothing more. The higher-level features your users expect — filenames, folders, search, sharing links, version history — are all built at the app layer on top of the SDK's simple, object-centric interface.

{% hint style="info" %}
**Design apps for portability and recovery.** Keep a current, usable cache of complete object records locally, and store the metadata needed to rebuild local app state on the indexer. After normal reauthorization, a surviving indexer plus the app's recovery phrase can rebuild the app; if the indexer is lost, a surviving local cache provides a last-resort way to seed a replacement without re-uploading object data. This fallback does not replace indexer backups, and losing both copies makes the object metadata unrecoverable.
{% endhint %}

{% hint style="info" %}
#### Building on Sia

Guides, SDK references, and the full app identity and onboarding model live in the [Sia Developer Portal](https://devs.sia.storage). Start with the [Quickstart](https://devs.sia.storage/docs/quickstart), then read the [Apps](https://devs.sia.storage/docs/core-concepts/apps) and [Indexers](https://devs.sia.storage/docs/core-concepts/indexers) concept pages.
{% endhint %}

## Why this matters: ownership without middlemen

Many services marketed as "decentralized" still place a company-operated gateway or proxy between you and the network. Your files pass through that server, which makes it a bottleneck, a logging point, and a single party that can inspect, throttle, censor, or simply disappear — recreating the dependence on a central operator that decentralization is supposed to remove. Sia's architecture removes that middleman, by design.

* **Your data never flows through a central server.** The SDK uploads and downloads encrypted shards **directly** to and from independent storage providers. The indexer coordinates *where* data lives and keeps it healthy, but it is never in the data path — it only ever handles encrypted metadata and the storage layout. There is no gateway that can see, meter, or gate your traffic.

* **You hold the keys, so you own the data.** Encryption and erasure coding happen on your own device before anything leaves it. Neither the indexer nor the storage providers can read your files, your metadata, or even your filenames. Even the apps you use are walled off from one another — each app has a distinct key derived during its approval, so one app cannot read another app's data even though both act on your behalf. Ownership is cryptographic — not a permission a provider grants you and can revoke.

* **No single operator can hold your data hostage.** Each object is erasure-coded into redundant shards spread across many unrelated storage providers worldwide, and only a subset is needed to reconstruct it. No one provider — and no outage, business failure, or demand against a single party — can read your data or take it offline.

* **You choose your indexer.** A well-designed app can move its cached metadata to another indexer while the encrypted sectors remain on their storage providers. Self-hosted operators should still maintain tested [`indexd` backups](setting-up-indexd/operations.md) for quick recovery of the indexer's operational state.

The result is storage that is genuinely distributed, private, and yours: no proxy in the middle, no operator that can read your data, and no provider that owns your access to it.

## The Marketplace

The Sia storage network is an open marketplace to connect consumers with providers for their data. The cost associated with this storage is competitively determined by storage providers and renters within the market. If providers discover that reducing prices allows them to secure more data for storage, they are inclined to do so. Similarly, if renters are willing to pay higher rates for storage with high-quality providers, those providers may opt to increase their prices.

The storage price is denominated in Siacoins, and you will need Siacoins to form storage contracts and upload data. Storage providers have the autonomy to establish their prices, fostering a competitive marketplace where top-quality and dependable providers vie for storage contracts from those seeking to store data. Network pricing averages around **$3 per terabyte per month,** including 3x redundancy.

## About contracts

Storage contracts are one of the most essential features of the Sia network. They allow the entire Sia ecosystem to work trustlessly – they form blockchain-enforced agreements between you and your storage providers that are automatically resolved when each party meets their obligation. In other words, they let you form contracts with people you don't know to store your data.

* **Storage providers** are responsible for data storage and receive compensation only after demonstrating successful storage for the agreed-upon period.
* **Indexers** form and renew those contracts on your behalf, paying providers for the storage you use.

Contract management is automatic. When you use [Sia Storage](https://sia.storage) or run your own [`indexd`](setting-up-indexd/), the indexer forms contracts as needed when you upload and renews them before they expire, so your data stays available without manual intervention.

## Fees

As a renter, you pay for the cost of storing data on the network. There are also some other fees that you're responsible for, such as:

* **Contract Formation Fees** – Creating storage contracts on the blockchain requires a transaction, and minimal fees are associated with this. Contract formation fees are one-time per contract and usually cost only a handful of Siacoins.
* **Bandwidth Fees** – You pay for the bandwidth you use to upload or download files. This can also include wear and tear fees set by the storage provider to help pay for their physical storage devices.

{% hint style="info" %}
#### Getting Started

For most people, the simplest way to start is the Sia Storage app with a free [Sia Storage](https://sia.storage) account (50 GB). To run the indexer yourself, see [Setting up indexd](setting-up-indexd/). Developers building applications can find the SDKs and guides in the [Sia Developer Portal](https://devs.sia.storage).
{% endhint %}
