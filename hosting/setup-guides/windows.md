---
description: Setup a new host on Windows
---

# ✏ Windows

This guide will walk you through setting up a new `hostd` node on Windows. For this guide, we are using Windows 11, but the steps should also work with Windows 10. At the end of this guide, you should have a working `hostd` node on the Sia network and be ready to accept contracts from renters.

## Things you'll need

Below are the minimum requirements for hosting on Sia. If you do not meet these requirements you may not receive contracts from renters or risk losing Siacoins as a penalty. Hosting is a commitment that requires some technical knowledge and a stable setup.

* Windows 10 or 11
* A quad-core CPU
* 8GB of RAM
* An SSD with a minimum of 64GB of free space.
* Additional storage space to rent out
* A stable internet connection

## Getting hostd

Download the latest version of `hostd` for your operating system and platform from the official website: [https://sia.tech/software/hostd](https://sia.tech/software/hostd).

For this guide, we will download the Windows version and unzip the `hostd` binary to `C:\hostd`

{% hint style="warning" %}
Windows Defender may flag \``` hostd` `` as a virus. This is a false positive. You can add an exception to Windows Defender (read more here: [https://go.dev/doc/faq#virus](https://go.dev/doc/faq#virus))
{% endhint %}

<figure><img src="../../.gitbook/assets/hostd_setup_windows_folder.png" alt=""><figcaption><p>hostd in the Windows file explorer</p></figcaption></figure>

## Creating a wallet

`hostd` uses BIP-39 12-word recovery phrases. It does not support legacy 28/29-word `siad` seeds. If you already have a 12-word seed, skip this step.

1. Open Explorer and browse to the folder where you unzipped `hostd.exe` (in our case `C:\hostd`)
2. Hold the SHIFT key and right-click in the folder, then click `Open command window here`

<figure><img src="../../.gitbook/assets/hostd_setup_windows_open_command_window.png" alt=""><figcaption><p>Open command window on Windows</p></figcaption></figure>

In the command prompt, run the following command to create a new wallet:

```
hostd.exe seed
```

<figure><img src="../../.gitbook/assets/hostd_setup_windows_cmd_seed.png" alt=""><figcaption><p>Generate a new recovery phrase</p></figcaption></figure>

After pressing enter, a new 12-word recovery phrase will be generated. Please write down this phrase and keep it in a safe place. You will need this phrase to recover your wallet. If you lose this phrase, you will lose access to your wallet and funds. You will also see the wallet's funding address. You can send Siacoin to this address to fund your host.

## Running hostd

In the same command prompt window you used to generate your recovery phrase, run the following command to start `hostd:`

```
hostd.exe
```

You will be asked to input a password and a wallet recovery phrase. The password is used to unlock the `hostd` UI, it should be something secure and easy to remember. The recovery phrase is the 12-word phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. These values are not stored anywhere; you will need to reenter them every time you start `hostd`.

{% hint style="info" %}
You can also set the `HOSTD_SEED` and `HOSTD_API_PASSWORD` environment variables so you do not have to reenter the values every time.
{% endhint %}

<figure><img src="../../.gitbook/assets/hostd_setup_windows_startup.png" alt=""><figcaption><p>hostd startup message</p></figcaption></figure>

After entering your password and recovery phrase, `hostd` will start. You can now access the `hostd` UI by opening a browser and going to `http://localhost:9980`. Enter your password to unlock `hostd`.

{% hint style="info" %}
You must leave the command prompt window open while `hostd` is running. If you close the command prompt window, `hostd` will stop.
{% endhint %}

<figure><img src="../../.gitbook/assets/hostd_setup_login_ui.png" alt=""><figcaption><p>hostd login</p></figcaption></figure>

## Updating

It is very important to keep your host up to date. New versions of hostd are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of hostd from https://sia.tech/software/hostd
2. Stop `hostd` in your command line by pressing `Ctrl+C`
3. Replace `hostd.exe` with the new version
4. Restart `hostd` in your command line
