# Listing Siacoin on your exchange

Sia is one of the best projects in the blockchain space. Sia is open source, and we believe completely in the spirit of decentralization. As such, exchanges should strive to implement the best projects that will enhance their platforms with little involvement from the development team for that project.

## Some background on Siacoin

Siacoin is used for buying and selling storage space on the Sia network. We believe that Siacoin is a pure utility token. Siacoin is generated only through Proof of Work mining, and there is no limit on the number of Siacoin that will be issued

## Download Sia

Siacoin is stored in a Sia wallet. Our two official apps are Sia-UI or siac (for command-line interfaces). Only one instance of Sia can run at a time, so you’ll need to install it on multiple machines or virtual environments if you’d like to run more than a single wallet.

{% hint style="info" %}
_If you would like to download and install the latest Sia wallet,_ [_you can do so here_](../../../your-sia-wallet/wallet-setup/sia-ui/how-to-download-and-install-sia-ui.md#find\_the\_right\_download\_for\_you)_._
{% endhint %}

## Technical Specifications for Sia

* **CPU:** Sia does not require any special CPU considerations
* **RAM:** +8 GB recommended
* **SSD:** +40 GB recommended (keep an eye on your consensus size!)

As of April 21, 2022, the block chain was \~34 GB, and you’ll need to download an entire copy to properly run your wallet. The blockchain grows by about 1 GB every two months.

No special libraries are required for installation.

## Review our API documentation

[Sia API docs](https://sia.tech/docs/)

## Setting up Sia

This is where you come in. Every platform is different, and your team can determine how best to integrate the Siacoin wallet. While we don’t provide dedicated technical support, our developers can provide assistance with your issues. See the "[Point of contact](listing-siacoin-on-your-exchange.md#point-of-contact)" section at the bottom of the article.

In the meantime, here are some answers to questions we’ve received regarding wallet setup for exchanges.

**IP Access Restriction.** IP access is restricted to localhost with user-agent "Sia-Agent" required. We highly recommended keeping this as the default.

**User Access Restriction.** Our API documentation has information on how to set up password authentication to access the API.

**Transactions per block.** We recommend at most three multi-output transactions per block, and about 250 outputs per multi-output transaction.

**TLS/SSL Availability.** TLS/SSL is not currently available.

**Transaction Fee.** The transaction fee is automatically set, but you can always get an estimated range [via the API](https://sia.tech/docs/#tpool-fee-get).

**If the explorer returns incorrect info.** Instead of using the explorer, use the /consensus endpoints listed in the API documentation. These should get you the same info easily. We'll be working on the explorer soon.

## Common API Requests

**Generating wallet addresses**

``[`/wallet/address [GET]`](https://sia.tech/docs/#wallet-address-get)``

**Getting transactions for an address**

[`/wallet/transactions/:addr [GET]`](https://sia.tech/docs/#wallet-transactions-addr-get)``

**Sending to an address or set of addresses**

``[`/wallet/siacoins [POST]`](https://sia.tech/docs/#wallet-siacoins-post)``

**Unlocking the wallet**

``[`/wallet/unlock [POST]`](https://sia.tech/docs/#wallet-unlock-post)``

**Verifying an address**

``[`/wallet/verify/address/:addr [GET]`](https://sia.tech/docs/#wallet-verify-address-addr-get)``

**Changing the wallet password**

``[`/wallet/changepassword [POST]`](https://sia.tech/docs/#wallet-changepassword-post)``

## A note about fees

We believe in the quality of our project, and the spirit of fair play. The long-term value proposition of listing any token comes, of course, from the transaction fees that an exchange earns. And these fees can add up to substantial amounts.

If your exchange requires any fee to list a coin, you can go ahead and skip us. We do not pay fees of any sort – whether they are called listing fees, marketing fees, sales budgets, etc.

## Community Votes

We don't participate in any type of community voting. Community votes typically come in two forms – those that are free and easy to manipulate or those that require paid votes and are still possible to manipulate. We'll never ask our community to participate in either in the future and urge all exchanges to add projects and tokens that they feel will benefit their users and the block chain space.

## A legal opinion

If your exchange requires an opinion regarding Siacoin's status as it relates to US securities law, you can [download our team's self-written opinion.](https://files.helpdocs.io/YzA4Zq3JuM/articles/4ubdozs16r/1531331962488/sia-legal-opinion-self-written.pdf) If your team requires an opinion from a US-based law firm, send an email to the point of contact listed below.

## Point of contact

If you have any questions, [send an email to Steve](mailto:steve@sia.tech). He runs our support channels and will get you in contact with our dev team.
