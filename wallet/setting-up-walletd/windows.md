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

# Windows Desktop App: `walletd`

The `walletd` desktop app provides a user-friendly web UI to start storing data on the Sia network. By the end of this guide, you will have:

* Installed the `walletd` desktop application.
* Created a `walletd` wallet.

## Pre-requisites

To run `walletd` on Windows, your system should meet the following specifications:

* **Network Access:** `walletd` requires a stable internet connection and open network access to store and retrieve data on the Sia network.
* **System Requirements:** Quad-core processor, 8GB RAM, and a minimum of 256GB SSD for consensus data.

## Download

1. Go to [Sia Software Downloads](https://sia.tech/software-downloads). Here you can find the latest software downloads for all our daemons.

![](../../.gitbook/assets/windows-walletd-app/sia-tech-website-download.png)

2. From the dropdown menu, select **Windows AMD64**.

![](../../.gitbook/assets/windows-walletd-app/walletd-download-website.png)

{% hint style="warning" %}
Before proceeding with downloading, please read our [Terms of Service](https://sia.tech/terms-of-service). Once you have reviewed and are satisfied, check the box to agree.
{% endhint %}

## Run

After downloading the `walletd` desktop application:

1. **Install the app:** Double-click the installer (e.g., `walletd.<version>.Setup.exe`) and follow the prompts. The app installs to the default location.
2. **Launch the app:** After installation, you can delete the installer, and launch `walletd` from the Start Menu like any other program.
3. **Initial setup *(first-time users only)*:** On first launch, the Welcome to `walletd` window will guide you to set a password to access web UI.

![](../../.gitbook/assets/windows-walletd-app/welcome-ui.png)

4. **Access the Web UI *(first-time users only)*:** Click **save and start daemon**. It will open automatically, or if not, you can access it at http://localhost:9980 while `walletd` runs in the background.

{% hint style="warning" %}
When you first run `walletd`, Windows Security may ask to allow public and private network access. This is normal—select **Allow** so `walletd` can communicate properly through the firewall.
{% endhint %}


![](../../.gitbook/assets/windows-walletd-app/web-ui.png)

{% hint style="success" %}
**Success!** `walletd` is now running on your Windows system, and you’re ready to start storing your data on the Sia network.
{% endhint %}

## Configure

You can customize `walletd` through the desktop app, which provides full control over all available settings, from wallet indexing to batch sizing and more.

On **Windows**, you can access the `walletd` configurations by going to the taskbar, expanding the up arrow to see hidden icons, and double-clicking the `walletd` app. This will open the configuration window and let you customize its behavior.

![](../../.gitbook/assets/windows-walletd-app/configuring.png)

There are several configurable settings in `walletd`. Below is a breakdown of what each setting does:

| Field | Description |
|------|-------------|
| Password | Set or update your wallet password |
| Automatically open the Web UI on startup | Enable this to launch the interface when `walletd` starts |
| Data Directory | Where `walletd` stores its data and config files |
| HTTP Address | Local address for the Web UI |
| Log Level | Amount of detail in logs |
| Index Mode | Indexing scope of either `personal` (your addresses), `full` (entire chain), or `none` (read-only). |
| Index Batch Size | Number of blocks processed per batch during indexing |
| Consensus Network | Connect to either `mainnet` (live network) or `zen` (test network) |
| Syncer Gateway Address | Address for connecting to a gateway node for syncing (optional) |
| Syncer Bootstrap | Enable for discovering and syncing with the network |
| Syncer Enable UPnP | Enable Universal Plug and Play (UPnP) to automatically configure router port forwarding for incoming connections |

{% hint style="warning" %}
Always **save and restart daemon** after making configuration changes to ensure they are applied.
{% endhint %}

You can monitor your node’s activity and track changes by checking the logs. These provide detailed information about the system, network connections, API endpoints, S3 interface, and autopilot operations, helping you understand what your node is doing at any given time.

![](../../.gitbook/assets/windows-walletd-app/config-logs.png)

## Update

`walletd` updates regularly with bug fixes, performance improvements, and new features. Updating your node ensures stability and compatibility with the Sia network. 

On Windows, the app downloads updates automatically and notifies you when they’re ready. Simply restart the app to run the latest version. 

{% hint style="info" %}
You can always check for the version of the software at the bottom of the app interface.
{% endhint %}

