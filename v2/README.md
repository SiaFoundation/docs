---
cover: https://sia.tech/assets/previews/nate-snow.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

The Sia network is hardforking to radically update Sia's consensus code, bringing huge benefits to performance, scalability, and functionality. Given the significance of this hardfork, we've come to refer to it as **Sia v2**.

Upgrading to Sia v2 will be necessary to send or store coins, rent, or host after the fork. Every user, exchange, mining pool, wallet, and integration should upgrade on the timelines found below.

## Step 1: Software release

The hardfork is multi-stage. First, hardfork-compatible software will release. Downloading this update means you're ready for the fork, even if the fork has not happened yet.

- For renters and hosts, the hardfork-compatible `renterd` and `hostd` will release in late December 2024.
- For Siacoin holders, miners, and exchanges, the hardfork-compatible walletd will release in January 2025.

You'll have from these dates until hardfork activation in mid-2025 to update, but we recommend doing it as soon as possible.

{% hint style="info" %}
If you haven't checked in for a while, in 2024 we split Sia into three distinct apps - `renterd` for renters who upload files, `hostd` for hosts who store those files, and `walletd` for Siacoin holders. You'll need to download and install each app if you use the associated function.

There are two versions of each app: The Desktop application, suitable for most users, and the Terminal application for advanced users. When the hardfork hits, your updated v2 version of Sia will instantly give you access to the new chain.
{% endhint %}

## Step 2:

The actual hardfork -- the point at which you *must* be running a v2 node -- occurs later in 2025. The Sia ecosystem is large, so we need to make sure that not only our users, but exchanges, miners and pools, web wallets, and other integrations have plenty of time to update.

- The hardfork activates on June 6th, 2025 at a block height of **526,000**. After this height, blocks may contain v2 transactions, so if you are not running an updated node, **you will not be able to sync**. This will enable most of the new v2 features, but v1 blocks are still allowed, giving any stragglers a grace period to submit their transactions to miners.
- This grace period ends on July 6th, 2025 at a block height of **530,000**. **You must update by this date to continue using Sia.**

## So how does the hardfork benefit...

### ...renters and hosts?

Sia v2 includes an update to the renter-host protocol that is faster and more efficient in almost every measurable way. Here are some highlights:
- Many more options and flexibility for your contracts
- Faster uploads and downloads, including concurrent uploads to the same host
- Enables decentralized uploads and downloads in a browser, no plugins or daemons necessary

It's important for renters and hosts to upgrade before June 6th so that they can enjoy the benefits of v2 and the new renter-host protocol as soon as possible.

### ...Siacoin holders?

First, to be absolutely clear: Your Siacoins are cryptographically owned by you, and Sia v2 doesn't change that. `walletd` is backwards-compatible, so you don't need to move your Siacoins to a new address in order to use them. That said, Sia v2 supports a new type of address that enables more flexible multisig scenarios and atomic swaps.

We recommend that Siacoin holders upgrade to `walletd` v2 by June 6th. If you don't, you'll still be able to broadcast transactions during the grace period, but you won't be able to sync new blocks. Regardless of your decision, your Siacoins are never at risk: they'll be available to spend again as soon as you update.

If you store Siacoins on an exchange, you don't have to do anything. The exchange is responsible for updating their nodes and ensuring that you can continue to deposit and withdraw Siacoins.

### ...for miners?

We've carefully designed Sia v2 to preserve to layout of block headers, so all mining hardware will remain compatible. You should, however, check in with your mining pool to make sure they've updated.

### ...for exchanges?

Sia v2 will enable highly increased performance and usability for your exchange. You'll have more control over your Siacoin treasury and the ways you interact with it.

Exchanges should upgrade to `walletd` v2 as soon as possible to ensure an issue-free transition. Due to the volume of users you serve, you should leave time for a proper upgrade. Once you do, your exchange will be able to support the fork once it takes effect.

Unconfirmed transactions as of block 526,000 will remain mineable until block 530,000, so normal operations can continue throughout the hardfork activation. If you are manually constructing your transactions, you have a choice of when to switch from using v1 transactions to v2 transactions; we recommend waiting at least 6 blocks into the grace period before switching. This minimizes the likelihood of v2 transactions being invalidated by a reorg.

# More questions?

Let us know! Send us an [email](mailto://hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
