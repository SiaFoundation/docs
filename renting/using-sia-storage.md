---
description: >-
  Get started with Sia Storage — hosted, end-to-end encrypted, decentralized
  storage with 50 GB free and nothing to run.
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

# Using Sia Storage

[Sia Storage](https://sia.storage) is a hosted **indexer** — the managed backend for storing data on Sia. It forms and manages storage contracts and keeps your data healthy for you, so there's no server, database, or contracts for you to run. To actually store and retrieve files, you point a **client** — the Sia Storage app or `s3d` — at your Sia Storage account.

Your files are still encrypted on your own device and erasure-coded across independent storage providers, as described in [About Storing Your Data](about-renting.md); Sia Storage only ever handles encrypted metadata, never your keys or file contents.

{% hint style="success" %}
**For almost everyone, this is the right place to start.** A Sia Storage account gives you **50 GB free**, with no infrastructure to run. You only need to self-host an [indexer](setting-up-indexd/) if you specifically want to control the backend yourself.
{% endhint %}

## Why Sia Storage

* **Private.** Files are encrypted on your device before they leave it, with keys derived from your recovery phrase. Neither Sia Storage nor the storage providers can read your data.
* **Decentralized.** Your data is stored across many independent storage providers, not in one company's data center, so no single operator or outage can read it or take it offline.
* **No infrastructure to run.** Sia Storage operates the indexer and manages contracts for you, so you can use the Sia network without running a server or database.

## Get started

1. Go to [sia.storage](https://sia.storage) and create an account. The free tier includes **50 GB** and up to **3 connected apps**.
2. Install a client and connect it to your account:
   * the **Sia Storage app** for desktop or mobile, or
   * **`s3d`** if you want an S3-compatible interface.
3. Use the client to upload and download your files.

<!-- SCREENSHOT NEEDED: Sia Storage sign-up / dashboard at sia.storage -->

Paid plans are available at [sia.storage](https://sia.storage) if you need more storage or connected apps.

## Ways to use it

* **Sia Storage app.** Apps for desktop (macOS, Linux, Windows) and mobile (iOS, Android) for storing and browsing your files.
* **S3-compatible access.** [`s3d`](https://github.com/SiaFoundation/s3d) is a gateway that exposes an S3-compatible API backed by your Sia Storage account, so existing S3 tools such as Rclone and Cyberduck can use Sia — see our [S3 integration guides](../sia-integrations/s3-integrations/).

## For developers

Sia Storage is also a hosted indexer your applications can build on. If you're building software on Sia, the [Sia Developer Portal](https://devs.sia.storage) covers the SDKs, the app identity model, and a [quickstart](https://devs.sia.storage/docs/quickstart) for uploading and downloading objects.

{% hint style="info" %}
Your application should let users choose where their data is stored rather than locking them to a single indexer. See [About Storing Your Data](about-renting.md#building-apps) for how applications, the SDK, and the indexer fit together.
{% endhint %}
