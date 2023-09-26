---
cover: ../../.gitbook/assets/sia-banner-expanded-walletd.png
coverY: 96.98442367601245
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

# ✏ Linux

This guide will walk you through setting up a `walletd` on Linux. At the end of this guide, you should have the following:

* **Installed Sia `walletd` software:** You should have successfully installed the Sia `walletd` software on your Linux operating system with the appropriate binary.
* **Functional Sia Wallet:** You should have a functional Sia wallet that is set up and ready for transactional use in the Sia network.
* **Basic Wallet Security:** You should have taken basic security measures, such as using a strong password for your wallet.

## Pre-requisites

* **Network Access:** `walletd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.
* **Operating System Compatibility:** Ensure that your Linux version is compatible with the walletd software. Check [releases](../../miscellaneous/releases.md) supported Linux versions.
* **System Updates:** Ensure that your Linux is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

{% hint style="info" %}
This guide primarily uses the command line and assumes the user has sudo permissions.
{% endhint %}

## Getting walletd

1. Download the latest version of `walletd` for your operating system from the [official website](https://sia.tech/software/walletd). For the purpose of this guide, we will download the Linux version and unzip the `walletd` binary to `/usr/local/bin`.

\<image>

```sh
unzip walletd_linux_amd64.zip
sudo mv -t /usr/local/bin walletd_linux_amd64/walletd
rm -rf walletd_linux_amd64.zip 
```

...

### Accessing the UI

For users with a desktop environment, you can open a browser to `http://localhost:9980` to access the `walletd` UI.

If you do not have a desktop environment:

1. Find your server's LAN IP using `ip addr`, `ifconfig`, etc.
2. Switch to another computer in your LAN and open the browser
3. Type your LAN IP followed by `:9980` in the address bar (e.g. `http://192.168.1.50:9980`)

\<image>

##

{% hint style="success" %}
Congratulations on successfully setting up walletd and taking a significant step towards securing your Siacoins. We invite you to explore our comprehensive [Wallet Overview](broken-reference), enabling you to become familiar with the UI and it's features.&#x20;
{% endhint %}

## Updating

It is very important to keep your host up to date. New versions of hostd are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of walletd from [https://sia.tech/software/walletd](https://sia.tech/software/walletd)
2. Stop the `walletd` service with the command `sudo systemctl stop walletd`
3. Unzip and replace `hostd` in `/usr/local/bin` with the new version
4. Restart `hostd` with `sudo systemctl start walletd`
