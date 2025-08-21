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

# Desktop App for Windows: `renterd`

The `renterd` desktop app provides a user-friendly web UI to start storing data on the Sia network. By the end of this guide, you will:

* Have installed `renterd` desktop application.
* Created a `renterd` wallet

## Pre-requisites

To run `renterd` on Windows, your system should meet the following specifications:

* **Network Access:**
  `renterd` requires a stable internet connection and open network access to store and retrieve data on the Sia network.

* **System Requirements:** Quad-core processor, 8GB RAM, and a minimum of 256GB SDD for consensus data.

{% hint style="warning" %}
We recommend 8GB of RAM, as `renterd` keeps full 120MB slabs in memory during uploads (often 2–3 at once). It can run with less, but performance depends on your use case.
{% endhint %}

## Download

1. Go to [Sia Software Downloads](https://sia.tech/software-downloads).

{% hint style="warning" %}
Before proceeding, please read our [Terms of Service](https://sia.tech/terms-of-service). Once you have reviewed and are satisfied, check the box to agree.
{% endhint %}

2. From the dropdown menu, select **Windows** and click **Download** to get the latest renterd version.

## Run

After downloading the `renterd` desktop application:

1. Locate the application in your **Downloads** folder. We recommend moving it to a convenient location.

2. Double-click the application. The web UI will open automatically, or you can access it at http://localhost:9980. `renterd` runs in the background.

![](../../.gitbook/assets/renterd-install-screenshots/macos/10-renterd-webui.png)

{% hint style="success" %}
**Success!**`renterd` is now running on your Windows system, and you’re ready to start storing your data on the Sia network.
{% endhint %}


## Configure

`renterd` can be customized by double-clicking the app, giving you full control over its behavior. Here’s what each setting means:"

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

On Windows, the app downloads updates automatically and notifies you when they’re ready. Simply restart the app to run the latest version. 

{% hint style="warning" %}
You can always check for the latest version at the bottom of the app interface.
{% endhint%}
