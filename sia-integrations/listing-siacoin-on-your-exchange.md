# Listing Siacoin on your exchange

Sia is one of the best projects in the blockchain space. Sia is open source and completely decentralized. As such, exchanges should strive to implement the best projects that will enhance their platforms with as little involvement from the development team for that project as possible.

## Some background on Siacoins

Siacoins are used for buying and selling storage space on the Sia network. We believe that Siacoins are a pure utility token. Siacoins are generated only through Proof of Work mining, and there is no limit on the number of Siacoins that will be issued.

## Download Sia

Siacoins are stored in a Sia wallet. Our two official apps are Sia-UI or siac (for command-line interfaces). Only one instance of Sia can run at a time, so you’ll need to install it on multiple machines or virtual environments if you’d like to run more than a single wallet.

You can download the latest release [directly from Github](https://github.com/SiaFoundation/siad/releases), or [from our website](https://sia.tech/get-started).

## Technical Specifications for Sia

* **CPU:** Sia does not require special CPU considerations
* **RAM:** 8 GB recommended
* **SSD:** 60 GB recommended (keep an eye on your consensus size!)

As of October 2022, the blockchain is 41.88 GB, and you’ll need to download an entire copy to run your wallet. The blockchain grows by about 1 GB every two months.

No special libraries are required for installation.

## Review our API documentation

[Sia API docs](https://sia.tech/docs/)

## Setting up Sia

This is where you come in. Every platform is different, and your team can determine how best to integrate the Siacoin wallet. While we don’t provide dedicated technical support, our developers can provide assistance with your issues. See the "[Point of contact](listing-siacoin-on-your-exchange.md#point-of-contact)" section at the bottom of the article.

In the meantime, here are some answers to questions we’ve received regarding wallet setup for exchanges.

**IP Access Restriction.** IP access is restricted to localhost with user-agent "Sia- Agent" required. We highly recommended keeping this as the default.

**User Access Restriction.** Our API documentation has information on how to set up password authentication to access the API.

**Transactions per block.** We recommend at most three multi-output transactions per block, and about 250 outputs per multi-output transaction.

**TLS/SSL Availability.** TLS/SSL is not currently available.

**Transaction Fee.** The transaction fee is automatically set, but you can always get an estimated range via the [API](https://api.sia.tech/#tpool-fee-get).

**If the explorer returns incorrect info.** Instead of using the explorer, use the /consensus endpoints listed in the API documentation. These should get you the same info easily. We'll be working on the explorer soon.

## Common API Requests

**Generating wallet addresses**

[https://api.sia.tech/#wallet-addresses-get](https://api.sia.tech/#wallet-addresses-get)

**Getting transactions for an address**

[https://api.sia.tech/#wallet-transactions-addr-get](https://api.sia.tech/#wallet-transactions-addr-get)

**Sending to an address or set of addresses**

[https://api.sia.tech/#wallet-siacoins-post](https://api.sia.tech/#wallet-siacoins-post)

**Unlocking the wallet**

[https://api.sia.tech/#wallet-unlock-post](https://api.sia.tech/#wallet-unlock-post)

**Verifying an address**

[https://api.sia.tech/#wallet-verify-address-addr-get](https://api.sia.tech/#wallet-verify-address-addr-get)

**Changing the wallet password**

[https://api.sia.tech/#wallet-changepassword-post](https://api.sia.tech/#wallet-changepassword-post)

## A note about fees

We believe in the quality of our project, and the spirit of fair play. The long-term value proposition of listing any token comes, of course, from the transaction fees that an exchange earns. And these fees can add up to substantial amounts.

If your exchange requires any fee to list a coin, you can go ahead and skip us. We do not pay fees of any sort – whether they are called listing fees, marketing fees, sales budgets, etc.

## Community Votes

We don't participate in any type of community voting. Community votes typically come in two forms – those that are free and easy to manipulate or those that require paid votes and are still easy to manipulate. We'll never ask our community to participate in either in the future and urge all exchanges to add projects and tokens that they feel will benefit their users and the blockchain space.

## A legal opinion

If your exchange requires an opinion regarding Siacoin's status as it relates to US securities law, you can contact our team for a copy of either our self-written opinion, or an opinion from a US-based law firm.

## Point of contact

If you have any questions, [send an email to Steve](mailto:steve@sia.tech). He runs our support channels and will get you in contact with our dev team.
