---
description: Setup a new host on macOS
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

# MacOS

This guide will walk you through setting up `hostd` on macOS. At the end of this guide, you should have the following:

* Installed Sia `hostd` software
* Created a `hostd` wallet

***

## Pre-requisites

To ensure you will not run into any issues with running `hostd` it is recommended your system meets the following requirements:

* **System Updates:** Ensure that your macOS version is up to date with the latest system updates. These updates can contain important security fixes and improvements.

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in fewer contracts from renters or the loss of collateral.
  - A quad-core CPU
  - 8GB of RAM
  - 256 GB SSD for `hostd`
    - 10 GB per 1 TB hosted for database storage
  - At least 4TB of HDD storage for renter data

* **Network Access:** `hostd` requires a stable internet connection and open network access to store and retrieve data on the Sia network.
  
* **Software Requirements:** Before installing `hostd`, you will need to install the [Homebrew](https://brew.sh) package manager. This will allow you to install and upgrade `hostd` easily.

## Installing `hostd`

Press `CMD + Space` to open Spotlight search and open a `terminal`.

![](<../../.gitbook/assets/hostd-install-screenshots/macos/00-hostd-open-terminal (1).png>)

{% hint style="warning" %}
Before you install `hostd`, make sure you have the [Homebrew](https://brew.sh) package manager installed.
{% endhint %}

Once the Terminal loads, use `brew` to install `hostd`:

```console
brew install siafoundation/sia/hostd
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/01-hostd-brew-install.png)

To confirm `hostd` has been installed, run the following:

```console
hostd version
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/hostd_version.gif)

## Configuring `hostd`

Now that you have `hostd` installed, you will need to create a seed phrase and admin password. To launch the built-in configuration wizard, run the following:

```console
hostd config
```

When the configuration wizard loads, you will be asked to verify the location of your data directory. If you would like to change this, you can do so now. Otherwise, type `no` to keep the default.

![](../../.gitbook/assets/hostd-install-screenshots/macos/hostd_config.gif)

Next, you will be asked to enter a seed phrase. If you already have one that you would like to use, you can enter it now. Otherwise, you can type `seed` to generate a new one. For the purpose of this guide, we will generate a new seed.

![](../../.gitbook/assets/hostd-install-screenshots/macos/03-hostd-generate-seed.png)

Next, you will be prompted to enter an admin password. This is used to unlock the `hostd` web UI.

![](../../.gitbook/assets/hostd-install-screenshots/macos/04-hostd-admin-password.png)

Finally, you will be asked if you want to configure advanced settings for `hostd`. Type `no` and hit enter to exit the configuration wizard.

![](../../.gitbook/assets/hostd-install-screenshots/macos/05-hostd-advanced-settings.png)

## Running `hostd`

Now that you have `hostd` successfully installed and configured, it is time to run it. Use the following command to start `hostd`:

```console
hostd
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/06-hostd-startup.png)

Once `hostd` has successfully started, the web UI should automatically open in your web browser.

{% hint style="info" %}
If the `hostd` web UI does not open. You can access it by opening your browser and going to [http://localhost:9980](http://localhost:9980/).
{% endhint %}

![](../../.gitbook/assets/hostd-install-screenshots/macos/07-hostd-webui.png)

{% hint style="success" %}
Congratulations, you have successfully set up `hostd`.
{% endhint %}

## Upgrading `hostd`

It is essential to keep your host up to date. New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

To upgrade your `hostd` to the newest version, make sure you have shut down `hostd` and then run the following:

```console
brew upgrade siafoundation/sia/hostd
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/08-hostd-upgrade.png)

You can confirm you have upgraded to the latest version using the following command:

```console
hostd version
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/09-hostd-version.png)

{% hint style="success" %}
Congratulations, you have successfully updated your version of `hostd`!
{% endhint %}
