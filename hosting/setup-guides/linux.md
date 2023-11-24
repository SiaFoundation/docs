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

# 🔧 Linux

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
wget https://sia.tech/downloads/latest/renterd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_linux_arm64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_arm64.zip
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
rm -rf hostd_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
unzip -j hostd_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen ARM64" %}
```console
unzip -j hostd_linux_amd64.zip hostd &&\
sudo mv -t /usr/local/bin hostd &&\
rm -rf hostd_linux_amd64.zip
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

## Configure Storage Drives

If you are storing your renter data on a separate storage device from your system, which is recommended, you will need to configure these drives to be mounted on boot.

To begin, you will need to locate the storage drive you would like to use for your renter's data.

```console
sudo fdisk -l
```

This will give a printout that looks similar to the following

```console
Disk /dev/sda: 476.94 GiB, 512110190592 bytes, 1000215216 sectors
Disk model: MTFDDAK512TDL-1A
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: FC9DFC63-D9B9-4418-98D3-B71A14D81DCC

Device       Start        End   Sectors   Size Type
/dev/sda1     2048       4095      2048     1M BIOS boot
/dev/sda2     4096    4198399   4194304     2G Linux filesystem
/dev/sda3  4198400 1000212479 996014080 474.9G Linux filesystem


Disk /dev/sdb: 5.47 TiB, 6001175125504 bytes, 11721045167 sectors 
Disk model: Expansion Desk   
Units: sectors of 1 * 512 = 512 bytes 
Sector size (logical/physical): 512 bytes / 4096 bytes 
I/O size (minimum/optimal): 4096 bytes / 4096 bytes 
Disklabel type: gpt 
Disk identifier: 95C65D62-CA73-934A-9C4B-030C5FF0321F 

Device     Start         End     Sectors  Size Type 
/dev/sdb1   2048 11721045133 11721043086  5.5T Linux filesystem
```

{% hint style="info" %}
For this guide we will be using the 5.5TiB storage drive listed as `/dev/sdb`
{% endhint %}

Now, you will also need to get the unique `UUID` and filesystem `TYPE` for the device you'd like to use. To do this run the following.

```console
sudo blkid
```

This will give you a printout similar to the following. Make sure to write down your `UUID` and filesystem `TYPE`, as you will need to reference these later on.

```console
sudo blkid
[sudo] password for sia: 
/dev/sdb1: UUID="4c95307e-ecdf-4376-bf6b-1ad006e6144b" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="Linux filesystem" PARTUUID="33f86d9c-8f52-4202-9bf9-4c83c76239e4"
```

Once you have your device's `UUID` and filesystem `TYPE`, you will then need to create a new mount point.

```console
sudo mkdir /mnt/sia-drive-01
```

Now, all that is left is to update the `/etc/fstab` with your new mount point so it can be mounted on boot.

To do this first open up your `fstab` in a text editor.

```console
sudo nano /etc/fstab
```

Once the editor loads, you will need to add the following on a new line at the bottom of the file.

* **UUID:** The device UUID of the drive that should be mounted (Example: `4c95307e-ecdf-4376-bf6b-1ad006e6144b`)
* **mount-point:** The directory where the contents of the drive can be accessed from (Example: `/mnt/sia-drive-01`)
* **fs-type:** The type of the file system (Example: `ext4`)
* **options:** Various mounting options, we use defaults which should be fine in most cases.
* **dump:** Number telling the system how often the drive should be backed up.
* **pass:** A number indicating the order in which the fsck program will check the devices for errors at boot time: `0` to avoid checking, `1` if this is the root file system, and `2` if this is any other device.

{% hint style="info" %}
`UUID`, `mount-point`, and `fs-type` are all required. If you are unsure what to use for `options`, `dump`, and `pass`. You can use `defaults 0 2` as shown in the example, or learn more about configuring your `fstab` [here](https://en.wikipedia.org/wiki/Fstab).
{% endhint %}

```console
UUID="4c95307e-ecdf-4376-bf6b-1ad006e6144b" /mnt/sia-drive-01 ext4 defaults 0 2
```

Save the file to disk using `ctrl+s` and exit the text editor using `ctrl+x`.


You can now verify it is working correctly by mounting the drive using the following.

```console
sudo mount -a
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

{% hint style="warning" %}
The port `9980` is `hostd`'s default operating port and should not need to be changed unless you require a custom configuration for your network.
{% endhint %}

{% tabs %}
{% tab title="Mainnet" %}
```yml
recoveryPhrase: your seed phrase goes here
http:
  address: :9980
  password: your_password
```
{% endtab %}

{% tab title="Testnet" %}
```yml
recoveryPhrase: your seed phrase goes here
http:
  address: :9880
  password: your_password
```
{% endtab %}
{% endtabs %}

Once you have added your recovery phrase and password save the file with `ctrl+s` and exit with `ctrl+x`.

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
If you are planning on using the zen testnet, make sure to change the `-http` flag to port `:9880`
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
