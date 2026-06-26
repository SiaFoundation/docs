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

# Your Sia Wallet

\
`walletd` is the Sia Foundation's standalone wallet for Siacoin (SC) and Siafunds. It can manage multiple wallets and supports Ledger hardware wallets, through either a command-line interface or a web interface.

`renterd`, `hostd`, and `indexd` each include a built-in wallet for the coins they spend. `walletd` is the separate, general-purpose wallet for holding and moving your own Siacoin, independent of those services.

`walletd` can index either just your own addresses or the entire chain, and it can hold your seed to send and receive or run watch-only — tracking addresses without access to private keys. Some of its features:

* Send, receive, and store Siacoins and Siafunds.
* Manage multiple wallets, including watch-only and Ledger hardware wallets.
* Track wallet balances and transaction history.
* Monitor the blockchain for activity on specific addresses.

{% hint style="info" %}
#### **Getting Started with `walletd`**

Start storing your Siacoins on Sia by downloading the official [`walletd` software](https://sia.tech/software/walletd) and exploring our step-by-step [Setting up walletd](setting-up-walletd/) guide.
{% endhint %}
