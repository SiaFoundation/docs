---
description: >-
  A step-by-step guide for setting up Nextcloud with renterd.
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

# Nextcloud

## What is Nextcloud?

Nextcloud is an open-source content collaboration platform. It’s like your own Cloud service that runs on your own hardware. You can use it for storing and sharing files through a web interface, mobile app, or desktop client, and even to collaborate with others or as a communication platform. There is almost no limit to what it can do with its open plugin store.

## Step 1: Install `renterd` and configure S3
This guide requires a working installation of `renterd`. If you have not already installed `renterd`, you will need to do so before continuing.
[**📖 `renterd` Installation Guide**](https://docs.sia.tech/v/current/renting/setting-up-renterd)


## Step 1: Enable `renterd` S3 API


## Step 2: Install `Nextcloud`



## Step 3: Configuring `Nextcloud`



## Step 4: Mount your bucket




{% hint style="info" %}
For more details and system-specific instructions, visit the official rclone mount documentation: [https://rclone.org/commands/rclone\_mount](https://rclone.org/commands/rclone\_mount/)
{% endhint %}

## All done.

We successfully used `renterd` and rclone to mount our Sia storage as a filesystem. This is a great way to use Sia for your files, especially for use cases such as large video or media libraries that take up many terabytes of space but you would still like available for streaming at any moment. If this guide has been engaging, check out our website to read more about Sia and `renterd`, and join our Discord, where the team and community can answer your questions!
