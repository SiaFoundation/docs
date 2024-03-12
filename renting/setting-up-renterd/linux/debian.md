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

This guide will walk you through setting up `renterd` on Linux. At the end of this guide, you should have the following:

* Installed the `renterd` software
* Created a `renterd` wallet

---


## Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

* **Network Access:** `renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

* **Operating System Compatibility:** `renterd` is supported on the following Debian versions:
	- Bookworm (Debian 12)
	- Bullseye (Debian 11)
	- Buster (Debian 10)

* **System Updates:** Ensure that Debian is up to date with the latest system updates, these updates can contain important security fixes and improvements.

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.
  - A dual-core CPU
  - 8 GB of RAM
  - An SSD with at least 128GB of free space.

{% hint style="warning" %}
To ensure proper functionality, we are recommending 8 GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
{% endhint %}

## Install `renterd` Using the `apt` repository

Before you install `renterd` for the first time on a new machine, you need to set up the Sia `apt` repository. Afterward, you can install and update `renterd` using `apt`.

**1. Set up the Sia `apt` repository by copying and pasting the following commands into your terminal:**

```sh
sudo curl -fsSL https://linux.sia.tech/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/siafoundation.gpg
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

**2. Install `renterd`**
```sh
sudo apt install renterd
```

![asdd](../../../.gitbook/assets/renterd-install-screenshots/linux/debian/02-renterd-debian-apt-install.png)

**3. Verify `renterd` was installed successfully**

Run the following command to see the version of `renterd` that was installed:

```sh
renterd version
```

![](../../../.gitbook/assets/renterd-install-screenshots/linux/debian/03-renterd-debian-version.png)

## Configure `renterd`

After installing `renterd`, you will need to configure it with a wallet seed and a password to unlock the web interface. There is an interactive configuration process that you can start by running the following command.

```sh
sudo mkdir /var/lib/renterd
cd /var/lib/renterd
sudo renterd config
```

This will start an interactive configuration process. You will be asked to generate or recover a wallet seed and set a password to unlock the web interface.

{% hint style="info" %}
You will not see anything when you type in your seed phrase or unlock password. Press enter after typing each one.
{% endhint %}

![](../../../.gitbook/assets/renterd-install-screenshots/linux/debian/04-renterd-debian-config.png)

## Start `renterd`

Now that you have installed and configured `renterd`, you can start it by running the following command:

```sh
sudo systemctl start renterd
```

## Updating `renterd`

New versions of `renterd` are released regularly and contain bug fixes and performance improvements.

**To update:**

1. Stop the `renterd` service.
```sh
sudo systemctl stop renterd
```

2. Upgrade `renterd` using the `apt` package manager.
```sh
sudo apt update
sudo apt upgrade renterd
```

3. Start `renterd` service.
```sh
sudo systemctl start renterd
```

## Next Steps

Now that you have `renterd` installed and running, you can start using it to store and retrieve data on the Sia network. You can access the web interface by navigating to `http://127.0.0.1:9980` in your web browser. If you installed `renterd` on a remote machine or a server, you will need to create an SSH tunnel to access the web interface.

- [About Renting](../../about-renting.md)
- [Transferring Siacoins](../../transferring-siacoins.md)
- [Managing Your Files](../../renting-storage/managing-your-files.md)
