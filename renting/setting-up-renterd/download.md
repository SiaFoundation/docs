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

# Download the Desktop Application `renterd`

The `renterd` desktop app provides a user-friendly web UI to start storing data on the Sia network. By the end of this guide, you will:

* Installed Sia `renterd` desktop application.
* Created a `renterd` wallet

## Pre-requisites

To run `renterd` smoothly, your system should meet the following specifications:

* **Network Access:**
  `renterd` requires a stable internet connection and open network access to store and retrieve data on the Sia network.

* **System Requirements:**
  - Quad-core processor
  - 8GB RAM
  - Minimum of 256GB SDD for consensus data.

{% hint style="warning" %}
We recommend 8GB of RAM, as `renterd` keeps full 120MB slabs in memory during uploads (often 2–3 at once). It can run with less, but performance depends on your use case.
{% endhint %}

## Download

1. Go to [Sia Software Downloads](https://sia.tech/software-downloads).

{% hint style="warning" %}
Before proceeding, please read our [Terms of Service](https://sia.tech/terms-of-service). Once you have reviewed and are satisfied, check the box to agree.
{% endhint %}

2. Select your operating system from the dropdown and click **Download** to get the latest `renterd` version.

## Run

After downloading the `renterd` desktop application:

1. Locate the application in your **Downloads** folder. We recommend moving it to a convenient location.**

2. Double-click the application. The web UI will open automatically, or you can access it at http://localhost:9980. `renterd` runs in the background.

![](../../.gitbook/assets/renterd-install-screenshots/macos/10-renterd-webui.png)

{% hint style="success" %}
Congratulations! `renterd` is now running on your system, and you’re ready to start storing your data on the Sia network.
{% endhint %}


## Configure

`renterd` can be customized to suit your preferences, giving you complete control over its behavior; these are what each setting means:

**Key Settings**
- Recovery Phrase: Your wallet recovery seed.
- Password: Set or update your wallet password.
- Automatically open the Web UI on startup: Enable this to launch the interface when renterd starts.

**Directories & Addresses**
- Data Directory: Where renterd stores its data and config files.
- HTTP Address: Local address for the Web UI
- Log Level: Amount of detail in logs

**S3 Settings**

- S3 Address: Local address and port for the S3 interface.
- S3 Interface: Local address and port for the S3 interface.
- S3 Disable Auth: Turn authentication on or off for S3.
- S3 Host Bucket: Optional default bucket name for S3 storage.


## Update

`renterd` updates regularly with bug fixes, performance improvements, and new features. Updating your node ensures stability and compatibility with the Sia network. 

On macOS and Windows, if the app is already installed, it downloads updates automatically and notifies you when they’re ready; simply restart the app to run the latest version, though you can also manually download and install the latest version if you prefer, though this isn’t necessary. 

You can always check for the latest version at the bottom of the app interface.

{% hint style="warning" %}
On Linux, automatic updates are currently __not__ supported, so you must update by downloading the latest version or using your package manager.
{% endhint%}