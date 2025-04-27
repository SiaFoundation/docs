---
cover: https://sia.tech/assets/previews/mountain.png
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

# Zen Testnet

The Sia Foundation has made a test environment available for users wishing to test hardforks, software developments, and integration within the Sia ecosystem via the Zen Testnet.

The Zen Testnet offers a secure environment to experiment with `renterd`, `hostd`, and `walletd`and explore the capabilities of Siacoin without the risk of losing real Siacoins, but also with no real-world value.&#x20;

## Running testnet

Running our software on the testnet is similar to running it on the mainnet. First, download the binary for [renterd](https://sia.tech/rent), [hostd](https://sia.tech/host), or [walletd](https://sia.tech/wallet) from our official website. Then, follow the same setup instructions for [renterd](../renting/setting-up-renterd/), [hostd](../hosting/setting-up-hostd/) or [walletd](../wallet/setting-up-walletd/), up until the point of running the software.

For Linux or macOS users, then simply run the software with the testnet runtime flag:

```
renterd --network=zen
hostd --network=zen
walletd --network=zen
```
## Funding your testnet address

With the availability of zSC, the [Zen Testnet faucet](https://zen.siascan.com/faucet) provides a convenient way to acquire zSC by simply providing your Sia wallet's address.

Once on the page, enter a Sia wallet address of either  `renterd`, `hostd`, or `walletd` , then enter the amount of Zen Siacoins (zSC) you wish to fund that address with.&#x20;

<figure><img src="../.gitbook/assets/zen faucet funding.png" alt=""><figcaption><p>Zen Testnet Faucet funding</p></figcaption></figure>

{% hint style="info" %}
It might take a minute or two for your wallet to be funded and for the transaction to appear in its transactions list.
{% endhint %}

## Block Explorer&#x20;

Our web-based block explorer and analytics tool is tailored for the Sia network. This comprehensive platform offers users a wide range of insights into the intricacies of the Siacoin network.&#x20;

Visit [SiaScan Zen](https://zen.siascan.com), our block explorer, to gain valuable insights into the testnet's activity, view transaction history, and monitor block confirmations.&#x20;

<figure><img src="../.gitbook/assets/siascan.png" alt=""><figcaption><p>Siascan Zen</p></figcaption></figure>

