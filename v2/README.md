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

# Sia's June 2025 Hardfork

The Sia network hardfork activated at block 526,000 on June 6th, 2025. All major ecosystem pools and exchanges supported the upgrade. We're still working with a small number of third parties to ensure full compliance.

## Details of the fork

The Sia network forked to radically update Sia's consensus code, bringing huge benefits to performance, scalability, and functionality. Given the significance of this hardfork, we've come to refer to it as **Sia v2**.

Upgrading to Sia v2 is necessary to send or store coins, rent, or host after the fork. Every user, exchange, mining pool, wallet, and integration must upgrade.

## What do I need to do?

If you use Sia and have not upgraded yet, now's the time. Renters, hosts, and wallet users should [update to the latest releases](https://sia.tech/upgrade-your-software) to get the most recent fork-compliant versions.

{% hint style="info" %}
If you haven't checked in for a while, in 2024 we split Sia into three distinct apps - `renterd` for renters who upload files, `hostd` for hosts who store those files, and `walletd` for Siacoin holders. You'll need to download and install each app if you use the associated function. Sia-UI and `siad` are deprecated and will not be updated.
{% endhint %}

### If you are using Sia Central's lite wallet

You do not need to do anything to support the fork.

### If you are holding tokens on an exchange

All exchanges that we are aware of have updated to support the fork, so your coins should be good to go. As always, we recommend never storing your tokens on an exchange long-term. You know the old saying: not your keys, not your coins.

### If you _are_ an exchange or mining pool

Upgrade to the latest version of `walletd`. Read our [upgrade guide](exchanges.md) for exchanges.

## How did it work?

### Step 1: Software release

The hardfork was multi-stage. First, users signaled support for the hardfork by updating to hardfork-compatible versions.

### Step 2: Hardfork activation

The actual hardfork -- the point at which you _must_ be running a v2 node -- occured at block 526,000 on June 6th, 2025. The Sia ecosystem is large, so we made sure that not only our users, but exchanges, miners and pools, web wallets, and other integrations had plenty of time to update.

* The hardfork activated at block height **526,000** on **June 6th, 2025**. After this height, blocks contained v2 transactions, so if you are not running an updated node, **you will not be able to sync**. This will enable most of the new v2 features.

### So how does the hardfork benefit...

#### ...renters and hosts?

Sia v2 includes an update to the renter-host protocol that is faster and more efficient in almost every measurable way. Here are some highlights:

* Many more options and flexibility for your contracts
* Faster uploads and downloads, including concurrent uploads to the same host
* Enables decentralized uploads and downloads in a browser, no plugins or daemons necessary

It's important for renters and hosts to upgrade if they have not already so that they can enjoy the benefits of v2 and the new renter-host protocol as soon as possible.

#### ...Siacoin holders?

Your Siacoins remain secured by your seed and don’t change with Sia v2. `walletd` is fully compatible with the existing blockchain data, so you're not required to move your coins to prevent loss. However, Sia v2 is deprecating support for legacy 28-word and 29-word seeds in favor of industry standard BIP39 12-word seed phrases.

`walletd` only supports the new 12-word seed format and does **not** support legacy 28-word or 29-word seeds. To ensure continued access to your coins, we **strongly recommend** generating a new 12-word seed and transferring your balance. Use the [SiaCentral Web Wallet](https://wallet.siacentral.com/) to create your new seed and Deposit Address.

* **If you're using a synced Sia-UI wallet:**\
  First send a small test amount (\~10 SC) to the new address to confirm it’s received. Then transfer the rest, leaving 1 SC behind if needed to cover the network fee.
* **If you don’t have a synced Sia-UI wallet:**\
  Log into SiaCentral with your 28/29-word seed and transfer your coins from there. SiaCentral will continue to support both old and new seed formats, but official apps will only support the new 12-word format.

We recommend that all Siacoin holders who have not upgraded to `walletd` to do so immediately.

#### ...for miners?

We've carefully designed Sia v2 to preserve the layout of block headers, so all mining hardware will remain compatible. You should, however, check in with your mining pool to make sure they've updated.

#### ...for exchanges?

Sia v2 will enable highly increased performance and usability for your exchange. You'll have more control over your Siacoin treasury and the ways you interact with it.

Exchanges should upgrade to `walletd` v2 as soon as possible to ensure an issue-free transition. Due to the volume of users you serve, you should leave time for a proper upgrade. Once you do, your exchange will be able to support the fork once it takes effect.

## More questions?

Let us know! Send us an [email](mailto:hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
