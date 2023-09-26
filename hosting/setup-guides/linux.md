---
description: Setup a new host on Linux
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

# ✏ Linux

This guide will walk you through setting up a new `hostd` node on Linux. For this guide, we are using Ubuntu, but the steps should work with most Linux distros. At the end of this guide, you should have a working `hostd` node on the Sia network and be ready to accept contracts from renters.

## Things you'll need

Below are the minimum requirements for hosting on Sia. If you do not meet these requirements you may not receive contracts from renters or risk losing Siacoins as a penalty. Hosting is a commitment that requires some technical knowledge and a stable setup.

* A Linux distro with `systemd` (Ubuntu, Debian, Fedora, Arch, etc)
* A quad-core CPU
* 8GB of RAM
* An SSD with at least 100GB of free space.
* Additional storage space to rent out
* A stable internet connection

`hostd` supports Linux/amd64 (most devices) and Linux/arm64 (Raspberry Pi, ROCKPro64, etc).

{% hint style="info" %}
This guide primarily uses the command line and assumes the user has sudo permissions. Desktop users can still open their favorite terminal and copy the commands.
{% endhint %}

## Getting hostd

Download the latest version of `hostd` for your operating system and platform from the official website: [https://sia.tech/software/hostd](https://sia.tech/software/hostd).

For this guide, we will download the Linux/amd64 version and unzip the `hostd` binary to `/usr/local/bin`

```
unzip hostd_linux_amd64.zip
sudo mv -t /usr/local/bin hostd_linux_amd64/hostd
rm -rf hostd_linux_amd64.zip 
```

## Creating a wallet

`hostd` uses BIP-39 12-word recovery phrases. It does not support legacy 28/29-word `siad` seeds. If you already have a 12-word seed, skip this step. Run the following command to generate a new wallet recovery phrase:

```
hostd seed
```

After pressing enter, a new 12-word recovery phrase will be generated. Please write down this phrase and keep it in a safe place. You will need this phrase to recover your wallet. If you lose this phrase, you will lose access to your wallet and funds. You will also see the wallet's funding address. You can send Siacoin to this address to fund your host.

```
hostd 5a7489b
Network Mainnet
Recovery Phrase: poet never rifle awake lunar during ocean eight dial gospel crazy response
Address addr:333d10486632f11c4c5b907c2e45d31478522dec525649712697404b4253e92ea5a84227187d
```

## Setting up a systemd service

Now that you have a recovery phrase, we will create a `systemd` service to run `hostd` on startup.

First, create a new environment file. Where you store the file is up to you, but you will need to know the path later. For this guide, we will store it in our home directory `/home/ubuntu/hostd.env`

```
sudo nano /home/ubuntu/hostd.env
```

Now, modify the file to add your wallet seed and API password. The password is used to unlock the `hostd` UI, it should be something secure and easy to remember. The recovery phrase is the 12-word phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step.

{% tabs %}
{% tab title="Mainnet" %}
```
HOSTD_SEED=potato never rifle awake lunar during ocean eight dial gospel crazy response
HOSTD_API_PASSWORD=sia is cool
```
{% endtab %}

{% tab title="Testnet" %}
```
HOSTD_ZEN_SEED=potato never rifle awake lunar during ocean eight dial gospel crazy response
HOSTD_ZEN_API_PASSWORD=sia is cool
```
{% endtab %}
{% endtabs %}

Next, we'll create the unit file to run `hostd`:

```
sudo nano /etc/systemd/system/hostd.service
```

Modify the following snippet to fit your host and paste it into the file. You must change the `User`, `EnvironmentFile` and data directory to fit your setup.

```
[Unit]
Description=hostd
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/hostd -dir /home/ubuntu/hostd -http :9980
Restart=always
RestartSec=15
User=ubuntu
EnvironmentFile=/home/ubuntu/hostd.env

[Install]
WantedBy=multi-user.target
Alias=hostd.service
```

Save the file and exit. Now it is time to start the service

```
sudo systemctl enable hostd
sudo systemctl start hostd
```

Your `hostd` service should now be running. You can check the status of the service by running the following command:

```
sudo systemctl status hostd
```

If the service was set up correctly it should say "active (running)."

### Accessing the UI

For users with a desktop environment, you can open a browser to `http://localhost:9980` to access the `hostd` UI.

If you do not have a desktop environment:

1. Find your server's LAN IP using `ip addr`, `ifconfig`, etc.
2. Switch to another computer in your LAN and open the browser
3. Type your LAN IP followed by `:9980` in the address bar (e.g. `http://192.168.1.50:9980`)

<figure><img src="../../.gitbook/assets/hostd_setup_login_ui.png" alt=""><figcaption><p>hostd login</p></figcaption></figure>

## Updating

It is very important to keep your host up to date. New versions of hostd are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of hostd from [https://sia.tech/software/hostd](https://sia.tech/software/hostd)
2. Stop the `hostd` service with the command `sudo systemctl stop hostd`
3. Unzip and replace `hostd` in `/usr/local/bin` with the new version
4. Restart `hostd` with `sudo systemctl start hostd`