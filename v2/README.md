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

# Things to Know

The Sia network is implementing a mandatory hardfork to radically update Sia's consensus code, bringing huge benefits to performance, scalability, and functionality.

The hardfork requires Sia v2 and is necessary to send or store coins, rent, or host after the fork. Every user, exchange, mining pool, wallet, and integration should upgrade on the timelines found below.

## Step 1: Software release

The hardfork is multi-stage. First, hardfork-compatible software will release. Downloading this update means you're ready for the fork, even if the fork has not happened yet.

- For renters and hosts, the hardfork-compatible renterd and hostd will release in late December 2024.
- For Siacoin holders, the hardfork-compatible walletd will release in January 2025.

You'll have from these dates until hardfork activation in mid-2025 to update, but we recommend doing it as soon as possible.

{% hint style="info" %}
If you haven't checked in for a while, in 2024 we split Sia into three distinct apps - renterd for renters who upload files, hostd for hosts who store those files, and walletd for Siacoin holders. You'll need to download and install each app if you use the associated function.

There are two versions of each app: The Desktop application, suitable for most users, and the Terminal application for advanced users. When the hardfork hits, your updated v2 version of Sia will instantly give you access to the new chain
{% endhint %}

## Step 2:

The actual hardfork occurs later in 2025. The Sia ecosystem is large, so we need to make sure that not only our users, but exchanges, miners and pools, web wallets, and other integrations have plenty of time to update.

- The hardfork activates on March 10, 2025 at a block height of **513,400**. This will enable most of the new v2 features, but doesn't break the old versions yet. We heavily recommend that all users are updated by this time...
- ...but you technically have until June 6th, 2025 at a block height of **526,000**. **You must be updated by this date to continue using or supporting Sia.**

## So what does the hardfork do...

### ...for renters and hosts?

It activates an awesome set of new features for Sia, making it faster and more efficient in almost every measurable way. Here's some highlights:
- Reduces the size of the blockchain on disk
- Atomic swaps with HTLC support
- Many more options and flexibility for your contracts
- Faster uploads and downloads
- Concurrent uploads
- Decentralized uploads and downloads in a browser without downloading software

**Renters and hosts should upgrade to v2 by March 10th.**

### ...for Siacoin holders?

First, one important thing. You'll have the exact same amount of Siacoins after the fork. If keeping your Siacoins safe is all you need, nothing much changes beyond that. Except the app will look a lot nicer.

We recommend that Siacoin holders upgrade to walletd v2 by March 10th. If you don't upgrade by the mandatory date of June 6th, you won't be able to send or receive coins on the new fork until you do. You never lose your coins. Once you update to the new chain, your coins will be available to you.​

If you store Siacoins on an exchange, you don't have to do anything... provided that exchange also updates to the new fork software. When an exchange updates their wallet, you'll now have the same amount of coins on the new Sia chain. These coins are usable to trade with exchanges once they have upgraded and to buy storage from hosts who also use the new chain.

### ...for miners?

Nothing will change. You should check in with your mining pool to make sure they've updated.

### ...for exchanges?

Sia v2 will enable highly increased performance and usability for your exchange. You'll have more control over your Siacoin treasury and the ways you interact with it.

The hardfork is mandatory as of block **526,000** on June 6th, so exchanges should upgrade to walletd v2 as soon as possible to ensure an issue-free transition. Due to the volume of users you serve, you should leave time for a proper upgrade. Once you do, your exchange will be able to support the fork once it takes effect.

Transactions created before the fork block but not confirmed yet will not be valid anymore after the fork block. We recommend that you pause withdrawals and don't send any transactions for the 6 hours leading up to the fork, and the 2 hours following the fork. This will prevent you from having your transactions become invalid.

# More questions?

Let us know! Send us an [email](mailto://hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
