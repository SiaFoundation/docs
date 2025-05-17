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

## How can I be ready for the fork?

### If you are a host

Upgrade to `hostd` v2.1.0+.

### If you are a renter

Upgrade to `renterd` v2.1.0+.

### If you are using Sia-UI or siad

Upgrade to `walletd` v2.4.1+.

### If you are using Sia Central's lite wallet

You do not need to do anything to support the fork.

### If you are holding tokens on an exchange

We recommend moving your Siacoin to a self-custodial wallet until after the hardfork activates to ensure uninterupted access to your Siacoin.

### If you are an exchange or mining pool

Upgrade to `walletd` v2.4.1+. Read our upgrade [guide](exchanges.md) for exchanges

## How does it work?

### Step 1: Software release

{% hint style="info" %}
If you haven't checked in for a while, in 2024 we split Sia into three distinct apps - `renterd` for renters who upload files, `hostd` for hosts who store those files, and `walletd` for Siacoin holders. You'll need to download and install each app if you use the associated function. Sia-UI and `siad` are deprecated and will not be updated.
{% endhint %}

The hardfork is multi-stage. First, users must signal support for the hardfork by updating to a hardfork-compatible version. Downloading this update means you're ready for the fork, even if the fork has not happened yet.

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

Your Siacoins remain secured by your seed and don’t change with Sia v2. `walletd` is fully compatible with the existing blockchain data, so you're not required to move your coins to prevent loss. However, Sia v2 is deprecating support for legacy 28- and 29-word seeds in favor of industry standard BIP39 12-word seed phrases.

`walletd` only supports the new 12-word seed format and does **not** support legacy 28- or 29-word seeds. To ensure continued access to your coins, we **strongly recommend** generating a new 12-word seed and transferring your balance. Use the [SiaCentral Web Wallet](https://wallet.siacentral.com/) to create your new seed and Deposit Address.

* **If you're using a synced Sia-UI wallet:**\
  First send a small test amount (\~10 SC) to the new address to confirm it’s received. Then transfer the rest, leaving 1 SC behind if needed to cover the network fee.
* **If you don’t have a synced Sia-UI wallet:**\
  Log into SiaCentral with your 28/29-word seed and transfer your coins from there. SiaCentral will continue to support both old and new seed formats, but official apps will only support the new 12-word format.

We recommend all Siacoin holders upgrade to `walletd` by **June 6th**. After that, you'll have a 1-month grace period to broadcast transactions, but syncing new blocks won't be possible. Starting **July 4th**, only software that supports v2 transaction signing—currently `walletd` and the SiaCentral Web Wallet—will work. Sia-UI will not be updated.

If you store Siacoins on an exchange, confirm that the exchange will support the fork. To ensure access to your tokens, we **strongly recommend** withdrawing them to a privately owned wallet before the fork.

#### ...for miners?

We've carefully designed Sia v2 to preserve the layout of block headers, so all mining hardware will remain compatible. You should, however, check in with your mining pool to make sure they've updated.

#### ...for exchanges?

Sia v2 will enable highly increased performance and usability for your exchange. You'll have more control over your Siacoin treasury and the ways you interact with it.

Exchanges should upgrade to `walletd` v2 as soon as possible to ensure an issue-free transition. Due to the volume of users you serve, you should leave time for a proper upgrade. Once you do, your exchange will be able to support the fork once it takes effect.

Unconfirmed transactions as of block 526,000 will remain mineable until block 530,000, so normal operations can continue throughout the hardfork activation. If you are manually constructing your transactions, you have a choice of when to switch from using v1 transactions to v2 transactions; we recommend waiting at least 6 blocks into the grace period before switching. This minimizes the likelihood of v2 transactions being invalidated by a reorg.

## More questions?

Let us know! Send us an [email](mailto:hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
