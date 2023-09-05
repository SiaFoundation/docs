# 📸 Windows

This guide will walk you through setting up a `walletd` on Windows. At the end of this guide, you should have the following:

* **Installed Sia `walletd` software:** You should have successfully installed the Sia `walletd` software on your Windows operating system with the appropriate binary.
* **Functional Sia Wallet:** You should have a functional Sia wallet that is set up and ready for transactional use in the Sia network.
* **Basic Wallet Security:** You should have taken basic security measures, such as using a strong password for your wallet.

## Pre-requisites

* **Network Access:** `walletd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.
* **Operating System Compatibility:** Ensure that your Windows operating system version is compatible with the walletd software. Check [releases](../../miscellaneous/releases.md) supported macOS versions.
* **System Updates:** Ensure that your Windows operating system is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

## Getting `walletd`

1. Download the latest version of `walletd` for your operating system from the [official website](https://sia.tech/software/walletd). For the purpose of this guide, we will download the Windows version and unzip the `walletd` binary to `C:\walletd`.

{% hint style="warning" %}
Windows Defender may flag `walletd` as a virus. This is a false positive. You can add an exception to Windows Defender. Read more [here](https://go.dev/doc/faq#virus).
{% endhint %}

\<image>

2. text
3. text

\<image>

4.

## Running `walletd`

1. In the same terminal, run the following command to start `walletd`:

```
walletd.exe
```

You will be prompted input a `API password`. This password is chosen by you and can be anything you want it to be. It will be used to unlock the `walletd` UI via your browser, it should be something secure and easy to remember. This value are not stored anywhere; you will need to re-enter it every time you start `walletd`.

2. After entering your desired  password, `walletd` will start.&#x20;

\<image>

3. You can now access the `walletd` UI by opening a browser and going to `http://localhost:9980`.



\<image>



{% hint style="warning" %}
You must leave the command prompt window open while `walletd` is running. If you close the command prompt window, `walletd`will stop.
{% endhint %}



\<image>



Enter your `API password` you created in the in the previous step to unlock `walletd`.

{% hint style="success" %}
Congratulations on successfully setting up walletd and taking a significant step towards securing your Siacoins. We invite you to explore our comprehensive [Wallet Overview](broken-reference), enabling you to become familiar with the UI and it's features.&#x20;
{% endhint %}

## Updating

It is very important to keep your host up to date. New versions of `walletd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Download the latest version of `walletd` from the [official website](https://sia.tech/software/walletd).
2. Stop `walletd` in your command line by pressing `Ctrl+C`
3. Replace `walletd.exe` with the new version
4. Restart `walletd` in your command line
