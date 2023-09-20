# ✏ Zen Testnet

The Sia Foundation has made a test environment available for users wishing to test hardforks, software developments, and integration within the Sia ecosystem via the Zen Testnet.

The Zen Testnet offers a secure environment to experiment with `renterd`, `hostd`, and `walletd`and explore the capabilities of Siacoin without the risk of losing real Siacoins, but also with no real-world value.&#x20;

{% hint style="warning" %}
Please ensure that you have already downloaded the correct testnet binary for either`renterd`, `hostd` or `walletd` compatible with your operating system from our [official website](https://sia.tech).&#x20;
{% endhint %}

## Running testnet via terminal

Running the Zen testnet for our Sia software is very similar to running it on the mainnet, however, we must specify the `-tags=testnet` flag in our terminal or console, to enable the test environment.&#x20;

### macOS

1. Open a terminal window and `path/to/the/<software>` folder. These folders will be called `renterd`, `hostd`, or `walletd` depending on which testnet you'd like to run.
2. Run the following command, which `<software>` is replaced with either `renterd`, `hostd`, and `walletd` :

```bash
go run -tags=testnet ./cmd/<software>
```

3. You will be prompted to input a `API password`. This password is chosen by you and can be anything you want it to be. It will be used to unlock the Zen testnet UI via your browser.&#x20;

{% hint style="info" %}
If you haven't done so yet, refer to the **Creating a Wallet** setup guides in the previous sections of the documentation. You'll specifically need this for generating a seed for `renterd` or `hostd`.
{% endhint %}

### Windows



### Linux



{% hint style="warning" %}
Remember to leave the terminal window open while `walletd` is running. If you close the command prompt window, `walletd`will stop.
{% endhint %}

## Funding your testnet address

With the availability of zSC, the [Zen testnet faucet](https://zen.siascan.com/faucet) provides a convenient way to acquire zSC by simply providing your Sia wallet's address.

Once on the page, enter the generated Sia wallet address of either `renterd`, `hostd`, or `walletd` , then enter the amount of Siacoins (SC) you wish to fund that address with.&#x20;

<figure><img src="../.gitbook/assets/zen faucet funding.png" alt=""><figcaption><p>Zen Testnet Faucet funding</p></figcaption></figure>

{% hint style="info" %}
It might take a minute or two for your wallet to be funded and for the transaction to pop up in the wallet's transactions list.
{% endhint %}

## Block Explorer

Users also have access to the block explorer. With the block explorer, users can dive into the intricacies of the Siacoin network, track transactions, and monitor block confirmations, gaining valuable insights into the testnet's activity.

\[[https://zen.sia.tech](https://zen.sia.tech/)].

