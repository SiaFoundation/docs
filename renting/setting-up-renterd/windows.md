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

# Windows Desktop App: `renterd`

The `renterd` desktop app provides a user-friendly web UI to start storing data on the Sia network. By the end of this guide, you will have:

* Installed the `renterd` desktop application.
* Created a `renterd` wallet

## Pre-requisites

To run `renterd` on Windows, your system should meet the following specifications:

* **Network Access:** `renterd` requires a stable internet connection and open network access to store and retrieve data on the Sia network.

* **System Requirements:** Quad-core processor, 8GB RAM, and a minimum of 256GB SSD for consensus data.

> **Note:** The system requirements for the `renterd` desktop app differ from the CLI version (which previously required a dual-core CPU, 16GB RAM, and 128GB SSD). The desktop app is optimized for a user-friendly experience and may require less RAM, but a faster processor and more storage are recommended for best performance. If you are running the CLI version, please refer to its documentation for specific requirements.
{% hint style="warning" %}
We recommend 8GB of RAM, as `renterd` keeps full 120MB slabs in memory during uploads (often 2–3 at once). It can run with less, but performance depends on your use case.
{% endhint %}

## Download

1. Go to [Sia Software Downloads](https://sia.tech/software-downloads). Here you can find the latest software downloads for all our daemons.

![](../../.gitbook/assets/windows-renterd-app/sia-tech-website-download.png)

2. From the dropdown menu, select **Windows AMD64**.

![](../../.gitbook/assets/windows-renterd-app/renterd-download-website.png)

{% hint style="warning" %}
Before proceeding with downloading, please read our [Terms of Service](https://sia.tech/terms-of-service). Once you have reviewed and are satisfied, check the box to agree.
{% endhint %}

3. Click **Download** to get the latest `renterd` version for your operating system.

## Run

After downloading the `renterd` desktop application:

1. **Install the app:** Double-click the installer (e.g., `renterd.<version>.Setup.exe`) and follow the prompts. The app installs to the default location.
2. **Launch the app:** After installation, you can delete the installer, and launch `renterd` from the Start Menu like any other program.
3. **Initial setup *(first-time users only)*:** On first launch, the Welcome to `renterd` window will guide you to generate a recovery phrase (which you can copy and lock) and set a password to access web UI.

![](../../.gitbook/assets/windows-renterd-app/welcome-ui.png)

4. **Access the Web UI *(first-time users only)*:** Click **save and start daemon**. It will open automatically, or if not, you can access it at http://localhost:9980 while `renterd` runs in the background.

{% hint style="warning" %} 
When you first run `renterd`, Windows Security may ask to allow public and private network access. This is normal—select Allow so walletd can communicate properly through the firewall. 
{% endhint %}

![](../../.gitbook/assets/windows-renterd-app/web-ui.png)

{% hint style="success" %}
**Success!** `renterd` is now running on your Windows system, and you’re ready to start storing your data on the Sia network.
{% endhint %}


## Configure

You can customize `renterd` through the desktop app, which provides full control over all available settings, from wallet security to network and S3 configurations.

On **Windows**, you can access the `renterd` configurations by going to the taskbar, expanding the up arrow to see hidden icons, and double-clicking the `renterd` app. This will open the configuration window and let you customize its behavior.

![](../../.gitbook/assets/windows-renterd-app/configuring.png)

There are several configurable settings in `renterd`. Below is a breakdown of what each setting does:

| Field | Description |
|------|-------------|
| Recovery Phrase | Your wallet recovery seed |
| Password | Set or update your wallet password |
| Automatically open the Web UI on startup | Enable this to launch the interface when `renterd` starts |
| Data Directory | Where `renterd` stores its data and config files |
| HTTP Address | Local address for the Web UI |
| Log Level | Amount of detail in logs |
| S3 Address | Local address and port for the S3 interface |
| S3 Interface | Enable or disable the S3 interface |
| S3 Disable Auth | Enable or disable authentication for S3 |
| S3 Host Bucket | Optional default bucket name for S3 storage |

{% hint style="warning" %}
Always **save and restart daemon** after making configuration changes to ensure they are applied.
{% endhint %}

You can monitor your node’s activity and track changes by checking the logs. These provide detailed information about the system, network connections, API endpoints, S3 interface, and autopilot operations, helping you understand what your node is doing at any given time.

![](../../.gitbook/assets/windows-renterd-app/config-logs.png)

## Update

`renterd` updates regularly with bug fixes, performance improvements, and new features. Updating your node ensures stability and compatibility with the Sia network. 

On Windows, the app downloads updates automatically and notifies you when they’re ready. Simply restart the app to run the latest version. 

{% hint style="info" %}
You can always check for the version of the software at the bottom of the app interface.
{% endhint %}