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

# About Providing Storage on Sia

**Providing storage** on Sia means contributing your excess storage space to the Sia network. You're helping to keep data where it belongs – safely in the hands of those who uploaded it, the **renters**.

You also earn Siacoins, the cryptocurrency that powers the Sia network. Siacoins can be used to purchase your storage space or converted to other cryptocurrencies or fiat on crypto exchanges.

Storage providers are a critical part of the ecosystem. You are contributing to the decentralized network that is the heart of Sia. Providing storage is also a more technical process than renting, and while anyone can reasonably easily set it up, there's a lot you'll want to know to maximize your setup.

## Pricing

As a host, you set your prices. There are a lot of specific price points you can control:

* **Storage Price:** The base price for your storage per TB/month.
* **Contract Fees:** A small, one-time fee per contract to cover network transaction costs.
* **Upload/Download Bandwidth Price:** Your price for upload or download bandwidth to and from your host per TB.
* **Collateral:** The amount of Siacoins you will lose if you don't fulfill the rental contract per TB/month.

## **About Contracts**

Storage contracts are one of the most essential features of the Sia network. They allow the entire Sia ecosystem to work trustlessly – they form blockchain-enforced contracts between you and the people who rent your storage space that is automatically fulfilled.

## Earn Siacoins

As a storage provider, you're part of a marketplace where you compete with other storage providers for renter contracts. Competition should drive prices down, and demand should drive prices up. The goal is a market where people can upload their data with maximum security, minimum cost, and at fair rates that provide revenue to the storage providers.

## Fees

As a storage provider, you earn Siacoin for the storage space that you sell. But you also put up collateral to create additional incentives for storage providers to be good and sustain a reliable network.

Having collateral incentivizes storage providers to be online and to keep their renter data intact. Storage providers that go offline or lose data lose their collateral, and hosts that stay online and keep data safe get their collateral back.

## Storage Provider Scoring

Your storage provider score is one of the most critical factors determining how you'll fare as a storage provider. This is based on several metrics – some that you can directly affect, some that improve or diminish over time based on your performance.

Sia is a decentralized network - the code to evaluate these scoring metrics is contained within each renter's Sia instance. For that reason, each Sia renter you encounter scores storage providers independantly, so you may be scored differently among different renters. As a storage provider, you do not have one overall score across the Sia network but many scores with many renters based on the metrics described below. Any website or service that benchmarks your storage node can only show you a score based on their own metrics, which may differ from what a renter comes up with.

### Specific Metrics

{% tabs %}
{% tab title="Storage Provider Uptime" %}
Collateral to storage provider uptime is a vital metric. It would be best if you were online when people try to get their data, and since that might be any time, you should be online all the time. You're allowed negligible downtime to address minor maintenance issues like restarting for updates, which could include approximately 14 hours per month.

In general, you should plan for your storage node computer to be turned on and online 24/7. If you can't commit to this, you shouldn't try to provide storage on the Sia network.

{% hint style="danger" %}
Warning: If you go offline for too long (less than 80% uptime) or lose renter data (by deleting it or experiencing a hardware failure), you can lose money by losing your collateral for active contracts. You can also become responsible for SiaFund fees for each contract.
{% endhint %}

Below are the exact amounts your score will change based on your uptime percentage. Greater than 98% uptime results in no penalty, the 14 hours a month explained above (2% of 720 hours in a month = 14 hours).

| Uptime | Score Multiplier | % Reduction in Score |
| ------ | ---------------- | -------------------- |
| 100%   | 1.0              | None                 |
| 98%    | 1.0              | None                 |
| 95%    | .91              | -10%                 |
| 90%    | .51              | -50%                 |
| 85%    | .16              | -85%                 |
| 80%    | .03              | -97%                 |

We could include more values in this table, but there's not much point. If you can't maintain a minimum of 95% uptime, becoming a storage provider is not for you.
{% endtab %}

{% tab title="Storage Pricing" %}
The storage price you set as a storage provider is one of the biggest ways you can affect your storage node's score. You want to set a price that's competitive, but that will still result in a reasonable amount of income for the space you offer. In general, the higher you price your storage, the lower your storage node's score will be. Your storage node's score will increase by a factor of 16 every time you cut your storage price in half. Decreasing your storage cost by even a small amount will have an impact on your score.

There are a number of other pricing factors you have to take into consideration as a storage provider:

* A **Contract Fee** is a one-time fee a renter pays in order to initiate a storage contract with you. It's intended to cover transaction fees on the Sia network related to the creation of the contract and receiving payments as a storage provider. This is normally set for you automatically, but it can be changed via the Terminal/command line. If you change it, you generally don't want to set this more than about 5 SC, as these costs are very low.
* **Bandwidth Price** can be set on a basis of SC per Terabyte transferred to/from your storage node. One price can be set for both upload and download bandwidth via the `hostd` UI, or different upload/download prices can be set individually via the Terminal/command line. It's suggested that you price your upload and download bandwidth in relation to your internet connection capabilities. If you have a fast connection such as gigabit fiber, you can price these items very low because a user transferring several Terabytes doesn't impact you very much. If you have a slow connection or data caps, you may want to consider a higher bandwidth price, though this may deter renters.
* Fees related to **Sector Access** and **RPC** are protections against malicious renters which may be trying to abuse storage providers by accessing resources without paying for uploading or downloading. These fees are capped at 1% of the cost to download a file, but some services which use Sia for storage may ignore your storage node if you set these fees to anything.
{% endtab %}

{% tab title="Collateral" %}
This is how many Siacoins you're willing to lose if you don't fulfill the rental contract, per TB. It's a guarantee to your renters that you will be online through the storage contract, and that you'll have their data intact at the end of the contract. As a storage provider, this is why you need Siacoins to start providing storage to the network. If you go offline for too long or lose renter data, you risk losing your collateral.

You should normally set your collateral to around **2-3x your base storage price** as a starting point in order to maximize your storage node's score in this area. For example, if you've priced your storage at 50 SC/TB, you should set your collateral at 100-150 SC/TB.

* If you set your collateral **too low**, your storage node's score will be reduced, because renters will have no reason to trust you as a storage provider if you have little or nothing to lose by going offline.
* If you set your collateral **too high**, this can also decrease your storage node's score. Renters pay a fee based on a percentage of your collateral that goes towards [Siafunds](https://docs.sia.tech/siafunds/learn-about-siafunds) - if your collateral is set very high, the fee a renter pays, as a result, will be very high, which can decrease your storage node's score.

**Monitoring Your Collateral**

You can view information on your collateral through the `hostd` dashboard.

![](../.gitbook/assets/hostd-screenshots/ui/hostd-dashboard-collateral.png)

With this information, you can determine how much collateral has been tied up in the hosting process, and adjust your collateral settings accordingly if necessary.
{% endtab %}

{% tab title="Storage Remaining" %}
The more free space you have, the more attractive you are to people who want to store things. It makes your storage node less likely to run out of space later. The scoring system takes this into account.

Again, each renter determines their score for your storage node. When a renter forms contracts with you, the more available space you have, the more reliable you look, and the higher this piece of the scoring will be.
{% endtab %}

{% tab title="Storage Node Age" %}
History matters. The longer you've been around, the more reliable you look to renters. Because of this, there's a penalty applied to new storage providers. How do you beat that penalty, you ask? Keep your storage node online.

Once you've been online for about twelve weeks, about half of the default contract length, your penalty disappears!

| Node Age (Blocks) | Node Age (Days) | Score Multiplier | % Reduction in Score |
| ----------------- | --------------- | ---------------- | -------------------- |
| 12,001            | 83.5            | 1.0              | 0%                   |
| 12,000            | 83              | .66667           | -33.33%              |
| 6,000             | 41              | .33333           | -66.67%              |
| 4,000             | 28              | .16667           | -83.33%              |
| 2,000             | 14              | .08333           | -91.667%             |
| 1,000             | 7               | .02778           | -97.222%             |
| 576               | 4               | .009259          | -99.0741%            |
| 288               | 2               | .0030864         | -99.69136%           |
| 144               | 1               | .0010288         | -99.89712%           |
{% endtab %}

{% tab title="Interaction Weight" %}
Interaction weight is a metric measured between your storage node and each renter on the Sia network. For example, if a renter tries to contact your storage node and you're frequently offline, your interaction score will decrease with that renter. Again, this score is unique for each renter you encounter - it will be different for each renter on the Sia network.

Keeping your storage node online will keep this score as high as possible.
{% endtab %}

{% tab title="Version Adjustment" %}
Stay updated. Your storage node score drops if you're not running the latest version of the Sia client. Sia is constantly under development, and bug fixes and new features are pushed out somewhat regularly. If you're running an older version of the client, your renters may not be able to take advantage of all the latest features of Sia until you upgrade.
{% endtab %}
{% endtabs %}

## Third-Party Storage Provider Scoring

We have an incredible community building on Sia. Third-party sites can develop their methods for scoring storage providers based on various metrics. For example, Sia Central has developed a [Host Browser](https://hosts.siacentral.com/), which allows you to browse and compare storage providers.

These benchmarks differ from the core Sia protocol but are still helpful and may be used to help monitor and improve your storage node over time.

Once you've started providing storage, you'll probably want to keep an eye on your storage node score and see how you might be able to improve your node's ranking.

{% hint style="info" %}
#### **Getting Started with `hostd`**

Contributing your storage space couldn't be any simpler by using Sia's `hostd` software!

Start providing storage on Sia with the official [`hostd` software](https://sia.tech/software/hostd) and exploring our step-by-step [Setting up hostd ](setting-up-hostd/)guide.
{% endhint %}
