---
description: >-
  This page discusses the basics of renting and the terms you need to know.
  Later pages walk you through the specific process.
cover: ../.gitbook/assets/renterd.png
coverY: 31.57632398753894
layout:
  cover:
    visible: true
    size: full
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

# About Renting on Sia

**Renting** on Sia means you upload files on the Sia storage network to other users who have made their space available, called **hosts**. The term **renter** is used to describe an individual or entity that creates storage contracts with **hosts**:

* To store a certain amount of data.
* For a certain period.
* For a certain amount of Siacoin (SC).

## The Marketplace

\
The Sia storage network is an open marketplace to connect consumers with providers for their data. The cost associated with this storage is competitively determined by hosts and renters within the market. If hosts discover that reducing prices allows them to secure more data for storage, they are inclined to do so. Similarly, if renters are willing to pay higher rates for storage with high-quality hosts, those hosts may opt to increase their prices.

The storage price is denominated in Siacoins, and you will need Siacoins to form storage contracts and upload data. Hosts have the autonomy to establish their prices, fostering a competitive marketplace where top-quality and dependable hosts vie for storage contracts from those seeking to store data. Network pricing averages around **$3 per terabyte per month,** including 3x redundancy.

## **About contracts**

Storage contracts are one of the most essential features of the Sia network. They allow the entire Sia ecosystem to work trustlessly – they form blockchain-enforced agreements between you and your storage providers that are automatically resolved when each party meets their obligation. In other words, they let you form contracts with people you don't know to store your data.

* **Hosts** are responsible for data storage and receive compensation only after demonstrating successful storage for the agreed-upon period.
* **Renters** are tasked with paying the host and are charged solely for the data storage they utilize.

By default, storage contracts last three months and automatically form when you upload your files.

## **Fees**

As a renter, you pay for the cost of renting storage space. There are also some other fees that you're responsible for, such as:

* **Contract Formation Fees** – Creating storage contracts on the blockchain requires a transaction, and minimal fees are associated with this. Contract formation fees are one-time per contract and usually cost only a handful of Siacoins.
* **Bandwidth Fees** – You pay for the bandwidth you use to upload or download files. This can also include wear and tear fees set by the host to help pay for their physical storage devices.

## **Autopilot and your Allowance**

By default, the Sia rentering software `renterd` runs with a module called `autopilot` enabled. `autopilot` is the software agent that automatically forms contracts based on your configured parameters. The most important parameter is your allowance; setting your allowance is the first thing you'll do when starting renting.

The allowance tells Sia how much Siacoin you're willing to spend on storage space and makes sure more than this amount is not deducted from your wallet. Setting your allowance too low might mean that Sia can't upload all your data or cannot form contracts with enough hosts. You can raise or lower your allowance at any time.

Setting your allowance happens before uploading files, and Sia automatically forms the contracts it needs with new hosts so that you can upload when you're ready. You might see multiple transactions hit your wallet right after setting your allowance – this is your Siacoins getting set aside with each host. Don't worry - you'll get whatever Siacoins you don't spend back at the end of the contract. With Sia, you only ever pay for what you use.

{% hint style="info" %}
## **Getting Started with `renterd`**

Start renting on Sia by downloading the official [renterd software](https://sia.tech/rent) and exploring our step-by-step [Setting up renterd](setting-up-renterd/) guide.
{% endhint %}
