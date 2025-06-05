---
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

This guide will walk you through setting up `walletd` on Linux. At the end of this guide, you should have:

* Installed Sia `walletd` software
* Created a `walletd` wallet

## Pre-requisites

* **Network Access:** `walletd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.
* **Operating System Compatibility:** Ensure your Linux version is compatible with the `walletd` software. Check [releases](../../miscellaneous/releases.md) supported by Linux versions.
* **System Updates:** Ensure that your Linux is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

## Getting `walletd`

{% hint style="warning" %}
Remember to check which version to download to ensure it works correctly with your operating system. To do this, run  `uname -m` in your Terminal Emulator.

* **x86\_64** - `Linux AMD64`
* **aarch64** - `Linux ARM64`
{% endhint %}

1. Download the latest version of `walletd` for your operating system from the [official website](https://sia.tech/software/walletd). For this guide, we'll be downloading the Linux version of `walletd` .
2. Now that we have downloaded `walletd`, it's recommended to unzip the `walletd` binary to `/usr/local/bin`. Right-click the unzip file, select **Open Terminal Here** to open your Terminal Emulator, and run the following commands:

```bash
unzip walletd_linux_arm64.zip
sudo mv -t /usr/local/bin walletd
rm -rf walletd_linux_arm64.zip 
```

{% hint style="info" %}
You'll be prompted to authorize this action by providing your system password. Type this in and press enter to continue.
{% endhint %}

3. Finally, for good practice, create a folder on the home drive. This folder will be utilized specifically to store data related to the `walletd` software. Open the Terminal Emulator and run the following command:

```bash
mkdir ~/walletd
```

## Running `walletd`

1. Run the following in your Terminal Emulator to start `walletd`:

```bash
 walletd
```

You will be prompted to input a `API password`. You choose this password, which can be anything you want. It will be used to unlock the `walletd` UI, via your browser, should be something secure and easy to remember. This value is not stored anywhere; you will need to re-enter it every time you start `walletd`.

{% hint style="info" %}
You can also set the `WALLETD_API_PASSWORD` environment variables so you do not have to re-enter the values every time.
{% endhint %}

2. After entering your desired `API password`, `walletd` will start.&#x20;

<figure><img src="../../.gitbook/assets/starting walletd.png" alt=""><figcaption><p>Starting walletd</p></figcaption></figure>

3. &#x20;You can now access the `walletd` UI by opening a browser and going to `http://localhost:9980`.&#x20;

{% hint style="warning" %}
Remember to leave the Terminal Emulator open while `walletd` it is running. If you close the command prompt window, `walletd` stop.
{% endhint %}

<figure><img src="../../.gitbook/assets/walletd login UI.png" alt=""><figcaption><p>walletd Login UI</p></figcaption></figure>

Enter your `API password` you created in the previous step to unlock `walletd`.

{% hint style="success" %}
Congratulations on successfully setting up `walletd` and taking a significant step towards renting storage space on the Sia network.
{% endhint %}

## Updating

New versions of `walletd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of `walletd` from the [official website.](https://sia.tech/wallet)
2. Stop the `walletd` service with `Crtl+C`.
3. Unzip and replace `walletd` with the new version.
4. Restart `walletd`.
