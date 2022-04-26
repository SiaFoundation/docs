# Delete your seed and make a new one

[Your seed is incredibly important](../../the-importance-of-your-seed.md), but there might be a time where you want to initialize your wallet with a new seed. Maybe you lost your old one, or maybe you're making a new wallet for a new purpose. Either way, we've got you covered.

## Things you'll need

* Sia installed on your computer
* A Sia wallet set up
* Siacoin, the cryptocurrency used to buy and sell storage

{% hint style="warning" %}
_This process generates a new wallet with a new Sia seed. This is not recommended if you currently have Siacoin in your wallet, unless you've already forgotten your Sia seed. Any Siacoin in your current wallet will no longer be accessible unless you have your previous seed and restore from it._
{% endhint %}

## Deleting your wallet and starting over

1. Go to the Terminal tab
2. Type: `wallet init --force`

{% hint style="warning" %}
_There are two dashes before the word `force`._
{% endhint %}

This will immediately erase your old wallet and create a new one. You will also see your new seed instantly in the Terminal window. [Make sure you safely store your new seed](../../the-importance-of-your-seed.md).

Go back to the Wallet tab, and use the new seed to unlock your wallet. Since this is a brand new wallet, your Siacoin balance will be 0 SC. Enjoy your new wallet!
