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

# Your Sia Seed

## About the Seed

Your Sia Seed holds the key to your Siacoin (SC) balance and access to your files. It is the most important information to keep safe when using Sia.

* Sia is using BIP 39 with 128 bits of entropy and is made up of 12 words to generate your Seed.
* Your Seed is generated when you first create your Siacoin wallet in `renterd`, `hostd` or `walletd`.
* You can always recover your Siacoin balance using your Sia Seed.

## Keeping your Seed safe

Keeping your Sia seed safe is important. Follow the proper procedures for securely storing it. Like any other valuable digital information, never rely on its safety unless you have multiple backups.

* **Use a Hardware Wallet:** Hardware wallets store seeds offline, which makes them less susceptible to attacks that require network access.
* **Create a Paper Backup:** Write down your Seed on paper and store it securely. Make multiple copies and keep them in different safe locations.
* **Use a Strong Password:** Encrypt your Seed with a strong and unique password and store it separately from the Seed.
* **Use a Biometric:** Keep your Seed in a biometric secure app that relies on Opt into using unique physical identity verification.
* **Memorize Your Seed:** If possible, memorize your Seed. However, ensure it's something you can remember accurately without writing it down.

{% hint style="warning" %}
An incorrectly written word or mistyped letter renders the entire Seed invalid, making it impossible to access your wallet or retrieve your Siacoins. Store it precisely as it was initially provided to you.
{% endhint %}

{% hint style="danger" %}
#### Lost or Stolen

If you lose your Seed, your Siacoin balance will become **permanently** inaccessible since Sia operates as a fully decentralized platform.

**The Sia development team cannot access your Seed under any circumstances.**

If someone steals your Seed, they can take your Siacoin balance. Be careful when sharing your Seed with any third party you do not fully trust.
{% endhint %}
