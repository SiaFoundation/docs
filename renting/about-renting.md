---
description: >-
  This page discusses the basics of renting and the terms you need to know.
  Later pages walk you through the specific process.
cover: ../.gitbook/assets/jungle.png
coverY: 0
---

# About Renting on Sia

**Renting** on Sia means you upload files on the Sia storage network to other users who have made their space available, called **hosts**. The term **renter** is used to describe an individual or entity that creates storage contracts with **hosts**:

* To store a certain amount of data.
* For a certain period of time.
* For a certain amount of Siacoin.

## The Marketplace

\
The Sia storage network is an open marketplace to connect consumers with providers for their data. The cost associated with this storage is competitively determined by hosts and renters within the market. If hosts discover that reducing prices allows them to secure more data for storage, they are inclined to do so. Similarly, if renters are willing to pay higher rates for storage with high-quality hosts, those hosts may opt to increase their prices.

The price of storage is denominated in Siacoins (SC), and you will need Siacoins (SC) to form storage contracts and upload data. Hosts have the autonomy to establish their own prices, fostering a competitive marketplace where top-quality and dependable hosts vie for storage contracts from those seeking to store data. Typically, network pricing averages around **$3 per terabyte per month** including 3x redundancy.

{% hint style="info" %}
Siacoin (SC) is a utility token whose sole purpose is to fulfill contracts on the Sia network.
{% endhint %}

## **About contracts**

Storage contracts are one of the most important features of the Sia network. They are what allow the entire Sia ecosystem to work in a trustless way – they form blockchain-enforced agreements between you and your storage providers that are automatically resolved when each party meets their obligation. In other words, they let you form contracts with people you don't know to store your data.

* **Hosts** are responsible for data storage and receive compensation only after demonstrating successful storage for the agreed-upon period of time.
* **Renters** are tasked with paying the host, and they are charged solely for the data storage they utilize.

By default, storage contracts last for three months and are automatically formed when you start uploading your files.

## **Fees**

As a renter, you pay for the cost of renting storage space. There are also some other fees that you're responsible for such as:

* **Contract Formation Fees** – Creating storage contracts on the blockchain requires a transaction, and there are very small fees associated with this. Contract formation fees are one-time per contract and usually cost only a handful of Siacoins (SC).
* **Bandwidth Fees** – You pay for the bandwidth you use when you upload or download files. This can also include wear and tear fees set by the host to help pay for their physical storage devices.

## **Autopilot and your Allowance**

By default, the Sia rentering software `renterd` runs with a module called `autopilot` enabled. `autopilot` is the software agent that automatically forms contracts based on your configured parameters. The most important parameter is your "allowance", setting your allowance is the first thing you'll do when starting renting.

The allowance tells Sia how much Siacoin you're willing to spend on storage space, and makes sure more than this amount is not deducted from your wallet. Setting your allowance too low might mean that Sia can't upload all your data, or might not be able to form the contracts with enough hosts. You can raise or lower your allowance at any time.

Setting your allowance happens before uploading files, and Sia starts to automatically form the contracts it needs with new hosts so that you can upload when you're ready. You might see multiple transactions hit your wallet right after setting your allowance – this is your Siacoins getting set aside with each host. Don't worry - you'll get whatever Siacoins that you don't spend back at the end of the contract. With Sia, you only ever pay for what you use.

{% hint style="info" %}
## **Getting Started with `renterd`**

Get started with renting on Sia by downloading the official [renterd software](https://sia.tech/rent) and exploring our step-by-step [Setting up renterd](setting-up-renterd/) guide.
{% endhint %}
