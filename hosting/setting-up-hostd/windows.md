---
description: Setup a new host on Windows
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

# Windows

This guide will walk you through setting up `hostd` on Windows. At the end of this guide, you should have the following:

* Installed Sia `hostd` software
* Functional `hostd` Node
* Created a `hostd` wallet

## Pre-requisites

* **Operating System Compatibility:** Ensure your Windows version is compatible with the `hostd` software. Check [releases](../../miscellaneous/releases.md) supported by Windows versions.

* **System Updates:** Ensure that your Windows is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

{% hint style="warning" %}
Your machine must meet the minimum requirements for providing storage on Sia. Not meeting these requirements may result in not receiving contracts from renters or risk losing Siacoins as a penalty. Being a storage provider on Sia is a commitment that requires some technical knowledge and a stable setup as such:

* Windows 10 or 11
* A quad-core CPU
* 8GB of RAM
* An SSD with at least 100GB of free space.
* Additional storage space to rent out
{% endhint %}

## Getting `hostd`

{% hint style="info" %}
You may need to run this step in administrative mode, so right-click **Command Prompt** and select **Run as administrator**.
{% endhint %}

1. Download the latest version of `hostd` for your operating system from the [official website](https://sia.tech/software/hostd). For this guide, we'll be downloading the Windows version of `hostd` .
2. Now that we have downloaded `hostd`, you may need to unzip it.
   * Right-click the downloaded `hostd` zip file and select **Extract All** to unzip it if it hasn't done so automatically. Select an accessible destination to extract the file.
   * Click on the newly unzipped directory.
3. Finally, for good practice, create a folder on the home drive. This folder will be utilized specifically to store data related to the `hostd` software. Open the **Command Prompt** and run the following command:

```bash
mkdir C:\Users\<your_username>\hostd
```

## Running `hostd`

1. Right-click the `hostd.exe` in the unzipped directory, and select **Run as administrator** to start `hostd`.

You will be prompted to input both:

* `password` - You choose this password, which can be anything you want. It will be used to unlock the `hostd` UI via your browser and API. This should be something easy to remember and at least 4 characters.
* `seed phrase` - The seed phrase is the 12-word phrase. Type it carefully, with one space between each word, or copy and paste it.

If you do not have a seed phrase, type **seed** to generate one. A new 12-word recovery phrase will be generated, so please copy and store it in a safe place, as you will need this phrase to recover your wallet.

These values are not stored anywhere and will be requested every time you start `hostd`.

{% hint style="warning" %}
If you lose this phrase, you will lose access to your wallet and funds. [Read more](../../get-started-with-sia/the-importance-of-your-seed.md) about the importance of your seed.
{% endhint %}

{% hint style="info" %}
You can also set the HOSTD`_SEED` and HOSTD`_API_PASSWORD` environment variables so you do not have to re-enter the values every time.
{% endhint %}

<figure><img src="../../.gitbook/assets/running hostd and generating a seed.png" alt=""><figcaption><p>Running hostd and generating a new seed</p></figcaption></figure>

2. After entering your desired `password` and `seed phrase`, `hostd` will start.

{% hint style="warning" %}
Windows Defender may flag`hostd`as a virus. This is a false positive, and you can **Allow access.** You can also add an exception to Windows Defender and read more about it [here](https://go.dev/doc/faq#virus).
{% endhint %}

<figure><img src="../../.gitbook/assets/Starting hostd.png" alt=""><figcaption><p>Starting hostd</p></figcaption></figure>

3. You can now access the `hostd` UI by opening a browser and going to `http://localhost:9980`.

{% hint style="warning" %}
Remember to leave the command prompt open while`hostd` it is running. If you close the command prompt window, `hostd` stop.
{% endhint %}

<figure><img src="../../.gitbook/assets/hostd UI.png" alt=""><figcaption><p>hostd Login UI</p></figcaption></figure>

Enter your `API password` you created in the previous step to unlock `hostd`.

{% hint style="success" %}
Congratulations on successfully setting up `hostd` and taking a significant step towards renting storage space on the Sia network.
{% endhint %}

## Updating

It is essential to keep your host up to date. New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of `hostd` from the [official website](https://sia.tech/software/hostd).
2. Stop the `hostd` service with `Crtl+C`.
3. Unzip and replace `hostd` with the new version.
4. Restart `hostd`.
