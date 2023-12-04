---
description: Setup a new host on Linux
cover: https://sia.tech/assets/previews/hostd.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

This guide will walk you through setting up `hostd` on Linux. At the end of this guide, you should have the following:

* Installed Sia `hostd` software
* Functional `hostd` Node
* Created a `hostd` wallet

## Pre-requisites

* **Network Access:** `hostd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.
* **Operating System Compatibility:** Ensure your Linux version is compatible with the `hostd` software. Check [releases](../../miscellaneous/releases.md) supported Linux versions.
* **System Updates:** Ensure that your Linux is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

{% hint style="warning" %}
Your machine must meet the minimum requirements for hosting on Sia. Not meeting these requirements may result in not receiving contracts from renters or risk losing Siacoins as a penalty. Hosting on Sia is a commitment that requires some technical knowledge and a stable setup such as:

* A Linux distro with `systemd` (Ubuntu, Debian, Fedora, Arch, etc)
* A quad-core CPU
* 8GB of RAM
* An SSD with at least 100GB of free space.
* Additional storage space to rent out
{% endhint %}

## Getting `hostd`

{% hint style="warning" %}
Remember to check which version to download to ensure it works correctly with your operating system. To do this, run  `uname -m` in your Terminal Emulator.

* **x86\_64** - `Linux AMD64`
* **aarch64** - `Linux ARM64`
{% endhint %}

1. Download the latest version of `hostd` for your operating system from the [official website](https://sia.tech/software/hostd). For this guide, we'll be downloading the Linux version of `hostd`. Open the Terminal Emulator and run the following command:
{% hint style="warning" %}
If you are installing `hostd` on a Raspberry Pi or other ARM64 architecture, or you intend to use the Zen Testnet. Make sure to download the correct binary for your system.
{% endhint %}

{% tabs %}
{% tab title="AMD64" %}
```console
wget https://sia.tech/downloads/latest/hostd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/hostd_linux_arm64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
wget https://sia.tech/downloads/latest/hostd_zen_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen ARM64" %}
```console
wget https://sia.tech/downloads/latest/hostd_zen_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

2. Now that we have downloaded `hostd`, we can unzip and extract the `hostd` binary to our `/usr/local/bin` directory
{% tabs %}
{% tab title="AMD64" %}
```console
unzip -j hostd_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
unzip -j hostd_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_linux_arm64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
unzip -j hostd_zen_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_zen_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen ARM64" %}
```console
unzip -j hostd_zen_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_zen_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

## Creating a wallet

`hostd` uses BIP-39 12-word recovery phrases. It does not support legacy 28/29-word `siad` seeds. If you already have a 12-word seed, skip this step. Run the following command to generate a new wallet recovery phrase:

```console
hostd seed
```

After pressing enter, a new 12-word recovery phrase will be generated. Please write down this phrase and keep it in a safe place. You will need this phrase to recover your wallet. If you lose this phrase, you will lose access to your wallet and funds. You will also see the wallet's funding address. You can send Siacoin to this address to fund your host.

```console
hostd 5a7489b
Network Mainnet
Recovery Phrase: poet never rifle awake lunar during ocean eight dial gospel crazy response
Address addr:333d10486632f11c4c5b907c2e45d31478522dec525649712697404b4253e92ea5a84227187d
```

## Setting up a systemd service

Now that you have a recovery phrase, we will create a new system user and `systemd` service to securely run `hostd` on startup.

First, we will create a new system user with `useradd` and disable the creation of a home directory. This is a security precaution that will isolate `hostd` from any unauthorized access to our system. We will then use `usermod` to lock the account and prevent anyone from logging in under the account.

```console
sudo useradd -M hostd &&\
sudo usermod -L hostd
```

Now we will create a new folder under `/var/lib/` titled `hostd` and give it the appropriate permissions. This folder will be utilized specifically to store data related to the `hostd` software. Open the Terminal Emulator and run the following commands:

```console
sudo mkdir /var/lib/hostd &&\
sudo chown hostd:hostd /var/lib/hostd &&\
sudo chmod o-rwx /var/lib/hostd
```

Next, create a file name `hostd.yml` file under `/var/lib/hostd/`

```console
sudo nano /var/lib/hostd/hostd.yml
```

Now, modify the file to add your wallet seed and API password. The recovery phrase is the 12-word phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `hostd` UI; it should be something secure and easy to remember.

{% tabs %}
{% tab title="Mainnet" %}
```yml
recoveryPhrase: your seed phrase goes here
http:
  password: your_password
```
{% endtab %}

{% tab title="Testnet" %}
```yml
recoveryPhrase: your seed phrase goes here
http:
  password: your_password
```
{% endtab %}
{% endtabs %}

Once you have added your recovery phrase and password, save the file with `ctrl+s` and exit with `ctrl+x`.

Next, we'll create a new system service to run `hostd` on startup:

```console
sudo nano /etc/systemd/system/hostd.service
```

Once the editor loads, copy and paste the following into it.

```toml
[Unit]
Description=hostd
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/hostd
WorkingDirectory=/var/lib/hostd
Restart=always
RestartSec=15
User=hostd

[Install]
WantedBy=multi-user.target
Alias=hostd.service
```

You can now save the file with `ctrl+s` and exit with `ctrl+x`.

{% hint style="warning" %}
If you are using external USB drives to store renter data, you will need to ensure that your drives are mounted during system boot. Not doing so could result in failed contracts and the loss of collateral.
{% endhint %}

## Running `hostd`

Now it is time to start the service

```console
sudo systemctl start hostd
```

Your `hostd` service should now be running. You can check the status of the service by running the following command:

```console
sudo systemctl status hostd
```

If the service was set up correctly, it should say "active (running)."

### Accessing the UI

For users with a desktop environment, you can open a browser to `http://localhost:9980` to access the `hostd` UI.

If you do not have a desktop environment:

1. Find your server's LAN IP using `ip addr`, `ifconfig`, etc.
2. Switch to another computer in your LAN and open the browser
3. Type your LAN IP followed by `:9980` in the address bar (e.g. `http://192.168.1.50:9980`)

<figure><img src="../../.gitbook/assets/hostd_setup_login_ui.png" alt=""><figcaption><p>hostd login</p></figcaption></figure>

## Updating

It is very important to keep your host up to date. New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of `hostd` from the [official website](https://sia.tech/software/hostd).
2. Stop the `hostd` service with `Crtl+C`.
3. Unzip and replace `hostd` with the new version.
4. Restart `hostd`.
