---
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

# Debian

This guide will walk you through setting up `hostd` on Linux. At the end of this guide, you should have the following:

* Installed the `hostd` software
* Created a `hostd` wallet

---


## Pre-requisites

To ensure you will not run into any issues with running `hostd` it is recommended your system meets the following requirements:

* **Network Access:** `hostd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

* **Operating System Compatibility:** `hostd` is supported on the following Debian versions:
	- Bookworm (Debian 12)
	- Bullseye (Debian 11)
	- Buster (Debian 10)

* **System Updates:** Ensure that Debian is up to date with the latest system updates, these updates can contain important security fixes and improvements.

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.
  - A quad-core CPU
  - 8GB of RAM
  - An SSD with at least 128GB of free space.

## Install `hostd` Using the `apt` repository

Before you install `hostd` for the first time on a new machine, you need to set up the Sia `apt` repository. Afterward, you can install and update `hostd` using `apt`.

**1. Set up the Sia `apt` repository by copying and pasting the following commands into your terminal:**

```sh
sudo curl -fsSL https://linux.sia.tech/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/siafoundation.gpg
sudo chmod 644 /usr/share/keyrings/siafoundation.gpg
echo "deb [signed-by=/usr/share/keyrings/siafoundation.gpg] https://linux.sia.tech/debian $(. /etc/os-release && echo "$VERSION_CODENAME") main" | sudo tee /etc/apt/sources.list.d/siafoundation.list
sudo apt update
```

{% hint style="info" %}
If you use a derivative distro, such as Kali Linux, you may need to substitute the part of this command that prints the version codename with the corresponding Debian release:

```sh
$(. /etc/os-release && echo "$VERSION_CODENAME")
```

Replace this part with the codename of the corresponding Debian release, such as bookworm.
{% endhint %}

![](../../../.gitbook/assets/renterd-install-screenshots/linux/debian/01-renterd-debian-apt-repo.png)

**2. Install `hostd`**
```sh
sudo apt install hostd
```

![asdd](../../../.gitbook/assets/hostd-install-screenshots/linux/debian/01-hostd-debian-apt-install.png)

**3. Verify `hostd` was installed successfully**

Run the following command to see the version of `hostd` that was installed:

```sh
hostd version
```

![](../../../.gitbook/assets/hostd-install-screenshots/linux/debian/02-hostd-version.png)

## Configure `hostd`

After installing `hostd`, you will need to configure it with a wallet seed and a password to unlock the web interface. There is an interactive configuration process that you can start by running the following command.

```sh
sudo mkdir /var/lib/hostd
cd /var/lib/hostd
sudo hostd config
```

This will start an interactive configuration process. You will be asked to generate or recover a wallet seed and set a password to unlock the web interface.

{% hint style="info" %}
You will not see anything when you type in your seed phrase or unlock password. Press enter after typing each one.
{% endhint %}

![](../../../.gitbook/assets/hostd-install-screenshots/linux/debian/03-hostd-debian-config.png)

## Start `hostd`

Now that you have installed and configured `hostd`, you can start it by running the following command:

```sh
sudo systemctl start hostd
```

## Updating `hostd`

New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

**To update:**

1. Stop the `hostd` service.
```sh
sudo systemctl stop hostd
```

2. Upgrade `hostd` using the `apt` package manager.
```sh
sudo apt update
sudo apt upgrade hostd
```

3. Start `hostd` service.
```sh
sudo systemctl start hostd
```

## Next Steps

Now that you have `hostd` installed and running, you can start using it to store and retrieve data on the Sia network. You can access the web interface by navigating to `http://127.0.0.1:9980` in your web browser. If you installed `hostd` on a remote machine or a server, you will need to create an SSH tunnel to access the web interface.

- [About Hosting on Sia](../../about-hosting-on-sia.md)
- [Adding Storage to `hostd`](../../adding-storage.md)
- [Announcing Your Host to the Sia Network](../../announcing-your-host.md)
- [Transferring Siacoins to Your Host Wallet](../../transferring-siacoins.md)
