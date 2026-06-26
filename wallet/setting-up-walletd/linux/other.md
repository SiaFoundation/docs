---
description: Setup a new wallet on Linux
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

# Linux

This guide will walk you through setting up `walletd` on Linux. At the end of this guide, you should have the following:

* Installed Sia `walletd` software
* Functional `walletd` Node
* Created a `walletd` wallet

## Pre-requisites

To ensure you will not run into any issues with running `walletd` it is recommended your system meets the following requirements:

* **Operating System Compatibility:** `walletd` is supported on the following Linux versions:
  - Trixie (Debian 13)
  - Bookworm (Debian 12)
  - Bullseye (Debian 11)
  - Plucky (Ubuntu 25.04)
  - Noble (Ubuntu 24.04)
  - Jammy (Ubuntu 22.04)

* **System Updates:** Ensure that your Linux system is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended.
  - A quad-core CPU
  - 8GB of RAM
  - 256 GB SSD for `walletd`

* **Network Access:** `walletd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.

## Install `walletd`

Download the latest version of `walletd` for your operating system from the [official website](https://sia.tech/software/walletd). For this guide, we'll be downloading the Linux version of `walletd`.

1. Open a terminal and download the latest version of `walletd` for your operating system.

{% tabs %}
{% tab title="AMD64" %}
```console
wget https://sia.tech/downloads/latest/walletd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/walletd_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

2. Now that we have downloaded `walletd`, we can unzip and extract the `walletd` binary to our `/usr/local/bin` directory

{% tabs %}
{% tab title="AMD64" %}
```console
unzip -j walletd_linux_amd64.zip walletd &&\
sudo mv -t /usr/local/bin walletd &&\
rm -rf walletd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
unzip -j walletd_linux_arm64.zip walletd &&\
sudo mv -t /usr/local/bin walletd &&\
rm -rf walletd_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

3. Create a new folder called `walletd`. This will hold all the runtime files `walletd` generates and uses.

    ```console
    mkdir /path/to/walletd/folder
    ```

## Configuring `walletd`

{% hint style="info" %}
`walletd` can manage multiple wallets, so the configuration wizard does not prompt for a seed. You create or import wallets from the web interface after `walletd` is running.
{% endhint %}

1. Before running the `walletd` configuration wizard, make sure to `cd` into the `walletd` runtime folder you created in the last section. Then run the `walletd` configuration wizard. This will generate a `walletd.yml` file that is used by `walletd` on start-up. You will be asked to set a password to unlock the web interface and optionally configure advanced settings such as the index mode.

    ```console
    cd /path/to/walletd/folder
    walletd config
    ```

## Start `walletd`

1. Once you have completed the configuration wizard, you can now start `walletd`.

    ```console
    cd /path/to/walletd/folder
    walletd
    ```

## Accessing the UI

For users with a desktop environment, you can open a browser to `http://localhost:9980` to access the `walletd` UI.

If you do not have a desktop environment:

1. Find your server's LAN IP using `ip addr`, `ifconfig`, etc.
2. Switch to another computer in your LAN and open the browser
3. Type your LAN IP followed by `:9980` in the address bar (e.g. `http://192.168.1.50:9980`)

![](../../../.gitbook/assets/walletd-screenshots/walletd-login.png)

## Updating

Keep your node up to date. New versions of `walletd` are released regularly and contain bug fixes and performance improvements.

**To update:**

1. Stop `walletd`.
2. Download the latest version of `walletd`.
{% tabs %}
{% tab title="AMD64" %}
```console
wget https://sia.tech/downloads/latest/walletd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/walletd_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

3. Unzip and replace `walletd` with the new version.
{% tabs %}
{% tab title="AMD64" %}
```console
unzip -j walletd_linux_amd64.zip walletd &&\
sudo mv -t /usr/local/bin walletd &&\
rm -rf walletd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
unzip -j walletd_linux_arm64.zip walletd &&\
sudo mv -t /usr/local/bin walletd &&\
rm -rf walletd_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

4. Start `walletd`.
    ```console
    cd /path/to/walletd/folder
    walletd
    ```

{% hint style="success" %}
You have updated your version of `walletd`.
{% endhint %}
