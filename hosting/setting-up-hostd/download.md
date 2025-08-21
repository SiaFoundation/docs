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

# Desktop App for Windows: `hostd`

The `hostd` desktop app provides a user-friendly web UI to start storing data on the Sia network. By the end of this guide, you will:

* Have installed `hostd` desktop application.
* Created a `hostd` wallet

## Pre-requisites

To run `hostd` on Windows, your system should meet the following specifications:

* **Network Access:** `hostd` requires a stable internet connection and open network access to provide storage on the Sia network.

* **System Updates:** Keep Windows updated to get the latest security fixes and improvements.

* **System Requirements:** Quad-core processor, 8GB RAM, a minimum of 256GB SDD for consensus data and 4TB HDD for stored data.

{% hint style="warning" %}
Storage providing is a commitment that requires technical knowledge, and your machine must meet Sia’s minimum requirements to avoid lost contracts or Siacoin penalties.
{% endhint %}

## Download

After downloading the `hostd` desktop application:

1. Locate the `.exe` in your **Downloads** folder. We recommend moving it to a convenient location.

2. Double-click the application. The web UI will open automatically, or you can access it at http://localhost:9980. `hostd` runs in the background.

![](../../.gitbook/assets/host_5.png)

{% hint style="success" %}
**Success!** `hostd` is now running on your Windows system, and you’re ready to start providing storage on the Sia network.
{% endhint %}

## Update

`hostd` updates regularly with bug fixes, performance improvements, and new features. Updating your node ensures stability and compatibility with the Sia network. 

On Windows, the app downloads updates automatically and notifies you when they’re ready. Simply restart the app to run the latest version. 

{% hint style="warning" %}
You can always check for the latest version at the bottom of the app interface.
{% endhint%}
