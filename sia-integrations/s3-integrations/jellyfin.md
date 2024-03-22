---
description: >-
  A step-by-step guide for setting up Jellyfin with renterd.
layout:
  cover:
    visible: true
    size: hero
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

# Jellyfin

## What is `Jellyfin`?

Jellyfin stands out as a free, open-source media server, offering a compelling alternative to proprietary platforms like Emby and Plex. It’s designed to give you complete control over organizing, managing, and streaming your media collection, which includes movies, TV shows, music, and photos. Its client/server model ensures cross-platform compatibility, enabling access to various devices, including desktops, smartphones, and smart TVs. The main allure of setting up Jellyfin is the autonomy it offers: you have complete control over your media, free from hidden fees or data tracking. Its user-friendly interface and robust community support make it highly customizable and continuously evolving. Jellyfin is ideal for creating a personal media hub, akin to having your own private Netflix, where your entire media library is organized and easily streamable to your chosen devices anywhere in the world. This combination of features makes Jellyfin not just a media server but a customizable, privacy-respecting solution that adapts to your growing media needs.

## Pre-Requisites

### Software:

* [**renterd**](https://sia.tech/software/renterd) — renterd is the next-generation Sia renter, which will function as a gateway to the Sia storage backend. With its powerful and user-friendly UI, we will use renterd to interface with the Sia network to store and retrieve our media files.
* [**rclone**](https://rclone.org/) — Rclone is a command-line program for managing files on cloud storage, supporting over 70 cloud storage products, including S3 object stores. Rclone will be used to integrate renterd with Jellyfin, facilitating the transfer and management of media files between the Sia network and the Jellyfin server.
* [**Jellyfin**](https://jellyfin.org/) — Jellyfin is a volunteer-built media solution that gives users control over their media content. Serving as the front-end media system, Jellyfin will allow us to stream and manage our media collection stored on the Sia network.
* [**Caddy Server (Optional)**](https://caddyserver.com/) — Caddy sports a flexible and powerful HTTP reverse proxy, an on-line configuration API, and a robust, production-ready static file server, and it serves all sites over HTTPS by default with automatic TLS certificates.

### Recommended System Requirements:

* **Processor:** A modern quad-core processor (Intel i5/i7 or equivalent AMD processor) or better.

* **Memory:** 16GB of RAM. More if handling high-quality media or numerous streams.

* **Storage:** SSD for the operating system and applications, with additional HDD or SSD storage for cached media files.

* **Network:** Stable, high-speed internet connection for effective streaming and data transfers.

* Operating System:

  * Windows 10 or later
  * MacOS 12 or later
  * Linux (Ubuntu, Debian, Fedora, CentOS, etc)

## Step 1: Install `renterd` and configure S3
This guide requires that you have a working installation of `renterd`. If you have not already installed `renterd`, you will need to do so before continuing.

{% hint style="warning" %}
Make sure to configure S3 when installing `renterd`, as this will be required later.
{% endhint %}

{% embed url="https://docs.sia.tech/v/current/renting/setting-up-renterd" %}

## Step 2: Install `rclone`

Install rclone and configure a new S3 remote using renterd for your storage backend.

{% embed url="https://docs.sia.tech/sia-integrations/s3-integrations/rclone" %}

## Step 3: Uploading Media

Once your renterd remote has been mounted on your system, you can begin uploading media. For the best experience, following the Jellyfin naming and sorting conventions is recommended. Doing so will help Jellyfin automatically obtain detailed metadata from various online databases. This includes cover art, media description, date, rating, related media, etc.

Below is an example of a properly structured file system following Jellyfin’s TV Shows and Movies standards.

![](../../.gitbook/assets/jellyfin-s3-integration/01-folder-structure.png)

## Step 4: Install `Jellyfin`

Download and install the Jellyfin server for your system.

{% embed url="https://jellyfin.org/downloads/server" %}

## Step 5: Configuring `Jellyfin` Server

Once you have installed the Jellyfin Server for your system, you can visit `http://localhost:8096` in your browser and follow the onscreen setup wizard to complete setting up your Jellyfin Server.

Select your preferred display language and click “Next”.

![](../../.gitbook/assets/jellyfin-s3-integration/02-jellyfin-welcome.png)

Create a `Username` and `Password`, then click “Next”.

![](../../.gitbook/assets/jellyfin-s3-integration/03-jellyfin-user-setup.png)

On the next screen, you will be asked to set up your media libraries. Since this guide uses two media types in our renterd bucket, TV Shows and movies, we will create a separate library for each. Click the “Add Media Library” card you see on the screen.

![](../../.gitbook/assets/jellyfin-s3-integration/04-jellyfin-media-libraries.png)

You will next be asked to select a `Content type`. We will begin by adding our TV Shows first. Select shows from the drop-down menu.

![](../../.gitbook/assets/jellyfin-s3-integration/05-jellyfin-content-type.png)

Next, enter a Display name and click the + to add your media.

![](../../.gitbook/assets/jellyfin-s3-integration/06-jellyfin-add-folder.png)

Enter the folder path to where your TV Shows are stored on your mounted `renterd` remote and click “Ok”.

![](../../.gitbook/assets/jellyfin-s3-integration/07-jellyfin-folder-path.png)

Finish configuring the rest of the `Library Settings` to your preferences, then click “Ok”.

![](../../.gitbook/assets/jellyfin-s3-integration/08-jellyfin-library-settings.png)

You will now see your TV Shows added to your media libraries. Repeat the process to add your Movies library and any others you might have. Then click “Next”.

![](../../.gitbook/assets/jellyfin-s3-integration/09-jellyfin-add-other-libraries.png)

Select the `Language` and `Country` you would like to use as the default for downloading your library’s metadata. Then click “Next”.

![](../../.gitbook/assets/jellyfin-s3-integration/10-jellyfin-language.png)

Configure Remote Access to your Server. If you are planning on accessing your libraries from another device on your network, you will need to have `Allow remote connections to this server` selected. You can then access your libraries using a Jellyfin client and the local IP of your Jellyfin server. Click “Next” when ready.

{% hint style="warning" %}
If you would like to access your Jellyfin libraries from outside your network, you should only do so using a secure `HTTPS` connection using [Caddy Server](https://caddyserver.com/).
{% endhint %}

![](../../.gitbook/assets/jellyfin-s3-integration/11-jellyfin-remote-access.png)

Congratulations! You have completed setting up your Jellyfin server. You can now click “Finish” and log in using the account you created initially.

![](../../.gitbook/assets/jellyfin-s3-integration/12-jellyfin-setup-complete.png)

## Step 6: Accessing your media collection

Once you have your Jellyfin server up and running, you can access your media collection from any device on your network using one of the available [Jellyfin Clients](https://jellyfin.org/downloads/clients/all).

{% embed url="https://jellyfin.org/downloads/clients/all" %}

After you have installed a Jellyfin client on your device, run the client app and follow the onscreen instructions to connect to your Jellyfin server.

Click "Add Server".

![](../../.gitbook/assets/jellyfin-s3-integration/13-jellyfin-client-connect.png)

Type in your server’s IP address, followed by port `8096` then click "Connect".

![](../../.gitbook/assets/jellyfin-s3-integration/14-jellyfin-host-address.png)

Next, enter your `User` name and `Password`, then click "Sign In.

![](../../.gitbook/assets/jellyfin-s3-integration/15-jellyfin-signin.png)

## All done.

Congratulations! You have successfully set up Jellyfin to stream your media collection from the Sia network.

![](../../.gitbook/assets/jellyfin-s3-integration/16-jellyfin-success.png)