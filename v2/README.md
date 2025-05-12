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

# Things to Know About Sia's Upcoming Fork

The Sia network is hardforking to radically update Sia's consensus code, bringing huge benefits to performance, scalability, and functionality. Given the significance of this hardfork, we've come to refer to it as **Sia v2**.

Upgrading to Sia v2 will be necessary to send or store coins, rent, or host after the fork. Every user, exchange, mining pool, wallet, and integration should upgrade on the timelines found below.

### Step 1: Software release

The hardfork is multi-stage. First, hardfork-compatible software will release. Downloading this update means you're ready for the fork, even if the fork has not happened yet.

* For renters and hosts, the hardfork-compatible `renterd` and `hostd` will release in late December 2024.
* For Siacoin holders, miners, and exchanges, the hardfork-compatible walletd will release in January 2025.

You'll have from these dates until hardfork activation in mid-2025 to update, but we recommend doing it as soon as possible.

{% hint style="info" %}
If you haven't checked in for a while, in 2024 we split Sia into three distinct apps - `renterd` for renters who upload files, `hostd` for hosts who store those files, and `walletd` for Siacoin holders. You'll need to download and install each app if you use the associated function.

There are two versions of each app: The Desktop application, suitable for most users, and the Terminal application for advanced users. When the hardfork hits, your updated v2 version of Sia will instantly give you access to the new chain.
{% endhint %}

### Step 2: Hardfork activation

The actual hardfork -- the point at which you _must_ be running a v2 node -- occurs later in 2025. The Sia ecosystem is large, so we need to make sure that not only our users, but exchanges, miners and pools, web wallets, and other integrations have plenty of time to update.

* The hardfork activates at block height **526,000** on or around **June 6th, 2025 06:00 UTC**. After this height, blocks may contain v2 transactions, so if you are not running an updated node, **you will not be able to sync**. This will enable most of the new v2 features, but v1 blocks are still allowed, giving any stragglers a grace period to submit their transactions to miners.
* This grace period ends at block height of **530,000** on or around **July 4th, 2025 02:00 UTC**. **You must update by this date to continue using Sia.**

### So how does the hardfork benefit...

#### ...renters and hosts?

Sia v2 includes an update to the renter-host protocol that is faster and more efficient in almost every measurable way. Here are some highlights:

* Many more options and flexibility for your contracts
* Faster uploads and downloads, including concurrent uploads to the same host
* Enables decentralized uploads and downloads in a browser, no plugins or daemons necessary

It's important for renters and hosts to upgrade before **June 6th** so that they can enjoy the benefits of v2 and the new renter-host protocol as soon as possible.

#### ...Siacoin holders?

Your Siacoins remain secured by your seed and don’t change with Sia v2. `walletd` is fully compatible with the existing blockchain data, so you're not required to move your coins to prevent loss. However, Sia v2 is deprecating support for legacy 28- and 29-word seeds in favor of a new industry-standard address format that supports more flexible multisig and atomic swaps.

`walletd` only supports the new 12-word seed format and does **not** support legacy 28- or 29-word seeds. To ensure continued access to your coins, we **strongly recommend** generating a new 12-word seed and transferring your balance. Use the [SiaCentral Web Wallet](https://wallet.siacentral.com/) to create your new seed and Deposit Address.

- **If you're using a synced Sia-UI wallet:**  
  First send a small test amount (~10 SC) to the new address to confirm it’s received. Then transfer the rest, leaving 1 SC behind if needed to cover the network fee.

- **If you don’t have a synced Sia-UI wallet:**  
  Log into SiaCentral with your 28/29-word seed and transfer your coins from there. SiaCentral will continue to support both old and new seed formats, but official apps will only support the new 12-word format.

We recommend all Siacoin holders upgrade to `walletd` by **June 6th**. After that, you'll have a 1-month grace period to broadcast transactions, but syncing new blocks won't be possible. Starting **July 4th**, only software that supports v2 transaction signing—currently `walletd` and the SiaCentral Web Wallet—will work. Sia-UI will not be updated.

If you store Siacoins on an exchange, confirm that the exchange will support the fork. While we’ll notify and assist exchanges, it’s their responsibility to upgrade their nodes. To ensure access to your tokens, we **strongly recommend** withdrawing them to a privately owned wallet before the fork.

#### ...for miners?

We've carefully designed Sia v2 to preserve the layout of block headers, so all mining hardware will remain compatible. You should, however, check in with your mining pool to make sure they've updated.

#### ...for exchanges?

Sia v2 will enable highly increased performance and usability for your exchange. You'll have more control over your Siacoin treasury and the ways you interact with it.

Exchanges should upgrade to `walletd` v2 as soon as possible to ensure an issue-free transition. Due to the volume of users you serve, you should leave time for a proper upgrade. Once you do, your exchange will be able to support the fork once it takes effect.

Unconfirmed transactions as of block 526,000 will remain mineable until block 530,000, so normal operations can continue throughout the hardfork activation. If you are manually constructing your transactions, you have a choice of when to switch from using v1 transactions to v2 transactions; we recommend waiting at least 6 blocks into the grace period before switching. This minimizes the likelihood of v2 transactions being invalidated by a reorg.

## More questions?

Let us know! Send us an [email](mailto:hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
