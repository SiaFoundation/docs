# Creating a new wallet

{% hint style="info" %}
_This guide assumes that you are setting up a new wallet in Sia-UI for the first time. If you need to restore an existing wallet,_ [_learn how here._](how-to-restore-a-wallet-from-a-seed-in-sia-ui.md)__
{% endhint %}

## Things You'll Need

* A computer with [the Sia-UI installed](how-to-download-and-install-sia-ui.md).
* A secure means of [storing your seed phrase](../back-up-your-sia-wallet.md).&#x20;

## Create a new wallet

When you first run the Sia-UI, you'll be prompted with two options. You can either create a new wallet or [restore a wallet from a seed](how-to-restore-a-wallet-from-a-seed-in-sia-ui.md). For this guide we will be creating a new wallet.

Click **Create new wallet.**

![](<../../../.gitbook/assets/restore-1 (2) (2) (2).png>)

Next, you'll be given your new seed phrase. Your seed is a string of (usually 29) words and is your key to your Siacoin wallet.

![](../../../.gitbook/assets/new-2.png)

**You need to keep your seed safe!** Safe means a lot of things to different people – but because your entire Siacoin balance is controlled by your seed, keep both digital and physical copies. Everyone does different things, and everyone has a different risk tolerance. Knowing this, our recommendations are as follows.

**Digitally:** Use a password or biometric (e.g. fingerprint) secured app like [1Password](https://1password.com/) or [LastPass](https://www.lastpass.com/).

**Physically:** Keep a laminated paper copy stored in a locked safe.

{% hint style="danger" %}
_**Loss:** If you lose your seed, your Siacoin balance will be unrecoverable._\
_**Theft:** If someone steals your seed, they can easily steal your Siacoin balance._
{% endhint %}

{% hint style="info" %}
_Ready for a deep dive?_ [_Learn more about the importance of your seed._](../../the-importance-of-your-seed.md)__
{% endhint %}



Once you've stored your seed, click **Next.**

You'll then be asked to verify your seed. The Sia-UI will ask you for a random selection of your 29 words to make sure you've copied them down correctly. Enter them in the appropriate blank spaces. You'll see each box outlined in green when you've entered them correctly, and you can go back to the previous screen if you need to double check.

Click **Done.**

![](../../../.gitbook/assets/new-3.png)

You might be asked to wait a moment while Sia-UI works.

![](../../../.gitbook/assets/new-4.png)

When Sia-UI is ready, you'll be taken the Dashboard. The Dashboard shows you a snapshot of the Sia network, including your current block height, the number of peers you're connected to, and the number of active hosts on the network.

These numbers will increase over time. Once you're caught up, block height grows by one every 10 minutes or so, active hosts will increase as more people lend their storage space to Sia, and active peers should stabilize around 7 or 8.

![](../../../.gitbook/assets/new-5.png)

When your block height is fully synced, you'll see **Synced** in the upper right corner. Hover over for more info.

![](../../../.gitbook/assets/new-6.png)

Your wallet is ready! Click on the Wallet tab to check it out.

![](../../../.gitbook/assets/send-1.png)

Once on the wallet screen you will be able to see your current balance, as well as send and receive siacoin.

Interested in what else your wallet can do? [Click here to learn more](../../wallet-overview.md).
