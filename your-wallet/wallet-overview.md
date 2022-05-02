# About your wallet

The Sia-UI and `siac` are not only the most secure ways to store your Siacoin. They're also your means to buying and selling storage space on the Sia network.

Your wallet also provides you with the tools needed to view your balance or transaction history, and to send or receive Siacoin.

{% hint style="info" %}
_`siac` is a_ [_command-line client_](../hosting/monitoring/cli/siac.md) _for Sia. It is only recommended for advanced users._
{% endhint %}

Here's what a typical Sia-UI wallet looks like.

![](../.gitbook/assets/send-1.png)

Your **balance** is at the top. This is the current amount of Siacoin in your wallet, and can fluctuate quite a bit depending on how you use Sia. If you own any Siafunds, they show up next to this.

## The Transactions tab

Every transaction is broken into a few categories - the Amount, Transaction ID, Time, TX Type, and Status.

![In this example, you can see three transactions.](../.gitbook/assets/wallet-1.png)

{% tabs %}
{% tab title="Amount" %}
The amount of Siacoin entering or leaving your wallet.
{% endtab %}

{% tab title="Transaction ID" %}
Use these to look up your transaction in a Sia blockchain explorer. The transaction IDs are shortened, but you can hover over them to see the full ID. You can also copy and paste while you do this.
{% endtab %}

{% tab title="Time" %}
The date and time the transaction was made.
{% endtab %}

{% tab title="TX Type" %}
The type of transaction that took place. Possible values are Siacoin, Siafund, Contract, Proof, Revision, Block, Defrag, and Setup.
{% endtab %}

{% tab title="Status" %}
While your transaction is confirming, you'll see 0/6, then 1/6, and so on. Once you reach six confirmations, you'll see the green checkmark like above and your transaction is considered confirmed.
{% endtab %}
{% endtabs %}

Near the upper right corner, you'll see a button that says `More`. Click on this to get some additional wallet options.

![](<../.gitbook/assets/wallet-2 (2) (3) (1).png>)

**View Seed** shows you your seed in case you need to see it again.

**Change Password** lets you set a custom password for your wallet, instead of using your Sia seed. [Learn about the pros and cons of a custom password.](wallet-setup/sia-ui/how-do-i-change-my-sia-wallet-password.md)

## Be careful

There are plenty of scams in the cryptocurrency space. Make sure the only software wallet you use to store your Siacoin is the official app downloaded from that link above or [our GitLab page.](https://gitlab.com/NebulousLabs/Sia-UI/tags) There are some other great recommendations you can get from [our community](https://discord.gg/sia), but we can't guarantee that any other software wallet will safely store your Siacoin.
