---
description: Setup a new host on macOS
cover: ../../.gitbook/assets/sia-banner-expanded-hostd.png
coverY: 144.86017518208027
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

# macOS

This guide will walk you through setting up `hostd` on macOS. At the end of this guide, you should have the following:

* Installed Sia `hostd` software
* Functional `hostd` Node
* Created a `hostd` wallet

## Pre-requisites

* **Network Access:** `hostd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.
* **Operating System Compatibility:** Ensure your macOS version is compatible with the `hostd` software. Check [releases](../../miscellaneous/releases.md) supported macOS versions.
* **System Updates:** Ensure that your macOS is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

{% hint style="warning" %}
Your machine must meet the minimum requirements for hosting on Sia. Not meeting these requirements may result in not receiving contracts from renters or risk losing Siacoins as a penalty. Hosting on Sia is a commitment that requires some technical knowledge and a stable setup as such

* A Mac that supports macOS 12 (Monterey) or 13 (Ventura)
* A quad-core CPU
* 8GB of RAM
* An SSD with at least 100GB of free space.
* Additional storage space to rent out
{% endhint %}

## Getting `hostd`

{% hint style="warning" %}
Remember to check which version to download to ensure it works correctly with your operating system. To do this, click on the Apple icon in the top left corner of your toolbar, then click **About This Mac**. If the processor/chips says:

* **Intel** - `MacOS AMD64`
* **M1 or M2** - `MacOS ARM64`
{% endhint %}

1. Download the latest version of `hostd` for your operating system from the [official website](https://sia.tech/host). For this guide, we'll be downloading the macOS version of `hostd` .
2. Now that we have downloaded `hostd`, you may need to unzip it.
   * Double-click the downloaded `hostd` zip file to unzip it if it hasn't done so automatically.
   * Click on the newly unzipped directory.
3. Finally, for good practice, create a folder on the home drive. This folder will be utilized specifically to store data related to the `hostd` software. It is essential to store `hostd`'s metadata on an SSD. You will need at least 80GB of space available. 50GB for the current blockchain and additional space for volume metadata. Run the following command to do so:

```bash
mkdir ~/hostd
```

## Running `hostd`

1. Click the `hostd` in the unzipped directory to start `hostd`.

{% hint style="warning" %}
You may encounter a warning stating **Your security settings only allow installation of apps from the App Store and identified developers**.&#x20;

To fix this issue, click on the Apple icon in the top left corner of your toolbar, then click **System Settings**. Once your System Settings is open, go to **Privacy & Security** and scroll down to the Security section. You will see a message **"hostd" was blocked from use because the identity of the developer cannot be confirmed.** This is a false positive.

Click **Open Anyway** and authenticate access either by your password or fingerprint.
{% endhint %}

You will be prompted to input both:

* `password` - You choose this password, which can be anything you want. It will be used to unlock the `hostd` UI via your browser and API. This should be something easy to remember and at least 4 characters.
* `seed phrase` - The seed phrase is the 12-word phrase. Type it carefully, with one space between each word, or copy and paste it.&#x20;

If you do not have a seed phrase, type **seed** to generate one. A new 12-word recovery phrase will be generated, so please copy and store it in a safe place, as you will need this phrase to recover your wallet.&#x20;

These values are not stored anywhere and will be requested every time you start `hostd`.

{% hint style="warning" %}
If you lose this phrase, you will lose access to your wallet and funds. [Read more](../../get-started-with-sia/the-importance-of-your-seed.md) about the importance of your seed.
{% endhint %}

{% hint style="info" %}
You can also set the HOSTD`_SEED` and HOSTD`_API_PASSWORD` environment variables so you do not have to re-enter the values every time.
{% endhint %}

<figure><img src="../../.gitbook/assets/running hostd and generating a seed mac.png" alt=""><figcaption><p>Running hostd and generating a seed</p></figcaption></figure>

2. After entering your desired `password` and  `seed phrase`, `hostd` will start.

<figure><img src="../../.gitbook/assets/starting hostd mac.png" alt=""><figcaption><p>Starting hostd</p></figcaption></figure>

Your terminal will produce a range of different values you may not be familiar with, so feel free to check the tabs below to see what each of them is and why they are essential:

{% tabs %}
{% tab title="api" %}
**api (Application Programming Interface) Component:**

* "api" refers to the application programming interface, which allows different software components to communicate and interact with each other.
* `Listening on 127.0.0.1:9980` indicates that the application's API component is actively waiting for incoming connections on the local loopback IP address `127.0.0.1` and the port `9980.`
{% endtab %}

{% tab title="p2p" %}
**p2p (Peer-to-Peer) Component:**

* "p2p" refers to the communication between different nodes or devices without relying on a central server.
* `Listening on 127.0.0.1:9981` means that the application's p2p component is currently set to listen for incoming network connections on the local loopback IP address `127.0.0.1` (also known as `localhost`) and the port `9981`. Localhost refers to the current machine itself,
{% endtab %}

{% tab title="rhp2" %}
**rhp2 (Remote Host Protocol - Version 2) Component:**&#x20;

* "rhp2" stands for Remote Host Protocol - Version 2, which pertains to a communication protocol between remote hosts without the necessity of a central server.&#x20;
* Being configured to listen on `127.0.0.1:9982` signifies that the application's rhp2 component is presently configured to accept incoming network connections on the local loopback IP address `127.0.0.1` (also recognized as `localhost`) and the port `9982.`
{% endtab %}

{% tab title="rhp3" %}
**rhp3 (Remote Host Protocol - Version 3):**&#x20;

* "rhp3" denotes using Remote Host Protocol - Version 3. This protocol allows remote hosts to communicate without relying on a centralized server.&#x20;
* Listening on `127.0.0.1:9983` through TCP implies that the application's rhp3 component is actively awaiting incoming connections on the local loopback IP address `127.0.0.1` and the port `9983` using the TCP protocol.
{% endtab %}

{% tab title="rhp3" %}
**rhp3 WebSocket (Remote Host Protocol - Version 3) over WebSocket**:&#x20;

* "rhp3 WebSocket" represents the implementation of Remote Host Protocol - Version 3 over the WebSocket communication protocol. This setup facilitates communication between remote hosts, eliminating the need for a central server.&#x20;
* Operating on `127.0.0.1:9984` via WebSocket designates that the application's rhp3 component is actively ready to accept incoming connections on the local loopback IP address `127.0.0.1` and the port `9984` using the WebSocket protocol.
{% endtab %}
{% endtabs %}

3. You can now access the `hostd` UI by opening a browser and going to `http://localhost:9980`.&#x20;

{% hint style="warning" %}
Remember to leave the terminal window open while `hostd` is running. If you close the terminal window, `hostd`will stop.
{% endhint %}

<figure><img src="../../.gitbook/assets/host_5.png" alt=""><figcaption><p>hostd Login UI</p></figcaption></figure>

Enter your `API password` you created in the in the previous step to unlock `hostd`.

{% hint style="success" %}
Congratulations on successfully setting up `hostd` and taking a significant step towards contributing your excess storage space to the Sia network.
{% endhint %}

## Updating

It is essential to keep your host up. New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of `hostd` from [https://sia.tech/software/hostd](https://sia.tech/software/hostd)
2. Stop the `hostd` service with `Cmd+C`.
3. Unzip and replace `hostd` in `/usr/local/bin` with the new version
4. Restart `hostd`.

