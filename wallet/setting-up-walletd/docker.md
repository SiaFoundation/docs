---
description: Setup a new wallet using Docker compose
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

# Docker Compose

This guide will walk you through setting up `walletd` using Docker compose. At the end of this guide, you should have the following:

* Installed Sia `walletd` software
* Created a `walletd` wallet

---

## Pre-requisites

To run `walletd` on Linux, your system should meet the following specifications:

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.
  - A quad-core CPU
  - 8GB of RAM
  - 256 GB SSD for `walletd`
  
* **Software Requirements:** Before installing `walletd`, you will need to install [Docker](https://www.docker.com/get-started/).

* **Network Access:** `walletd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.

## Create the compose file

Create a new file named `docker-compose.yml`. You can use the following as a template. The `/data` mount is where consensus data is stored and is required.

```yml
services:
  walletd:
    container_name: walletd
    image: ghcr.io/siafoundation/walletd:latest
    restart: unless-stopped
    ports:
      - 127.0.0.1:9980:9980/tcp
      - 9981:9981/tcp
    volumes:
      - walletd-data:/data

volumes:
  walletd-data:
```

{% hint style="warning" %}Be careful with port 9980 as Docker will expose it publicly by default. It is recommended to bind it to 127.0.0.1 to prevent unauthorized access. If you need to expose it to a LAN, ensure the port is not accessible publicly.{% endhint %}

## Getting the `walletd` image

To get the latest `walletd` image run the following command:
```
docker compose pull
```

![](../../.gitbook/assets/walletd-screenshots/install/docker/01-walletd-docker-pull.png)

## Configuring `walletd`

Now that you have the latest `walletd` image downloaded, you will need to create a seed phrase and admin password. To launch the built-in configuration wizard, run the following:

```console
docker compose run --rm -it walletd config
```

![](../../.gitbook/assets/walletd-screenshots/install/docker/walletd-docker-config.gif)

When the configuration wizard loads, you will be asked to verify the location of your data directory. Type `no` to keep the default.

![](../../.gitbook/assets/walletd-screenshots/install/docker/02-walletd-docker-config-data-dir.png)

Next, you will be prompted to enter an admin password. This is used to unlock the `walletd` web UI.

![](../../.gitbook/assets/walletd-screenshots/install/docker/03-walletd-docker-config-password.png)

Finally, you will be asked if you want to configure advanced settings for `walletd`. Type `no` and hit enter to exit the configuration wizard.

![](../../.gitbook/assets/walletd-screenshots/install/docker/04-walletd-docker-config-advanced-settings.png)

## Running `walletd`

Now that you have `walletd` successfully installed and configured, it is time to run it. Use the following command to start `walletd`:

```console
docker compose up -d
```

![](../../.gitbook/assets/walletd-screenshots/install/docker/05-walletd-docker-started.png)

Once `walletd` has successfully started, you can access the web UI by opening your browser and going to [http://localhost:9980](http://localhost:9980/).

![](../../.gitbook/assets/walletd-screenshots/walletd-login.png)

{% hint style="success" %}
Congratulations, you have successfully set up `walletd`.
{% endhint %}

## Checking the container status

To check the status of the container run:
```
docker ps -a
```

If the container is not running, it will show in the `STATUS` column

![](../../.gitbook/assets/walletd-screenshots/install/docker/06-walletd-docker-status.png)

## Checking the logs

To check the container logs run:
```
docker compose logs walletd
```

![](../../.gitbook/assets/walletd-screenshots/install/docker/07-walletd-docker-logs.png)

## Upgrading `walletd`

It is essential to keep your `walletd` up to date. New versions of `walletd` are released regularly and contain bug fixes and performance improvements.

To upgrade your `walletd` to the newest version, make sure you have shut down `walletd` and then run the following:

```console
docker compose pull && docker compose up -d
```

![](../../.gitbook/assets/walletd-screenshots/install/docker/08-walletd-docker-upgrade.png)

{% hint style="success" %}
Congratulations, you have successfully updated your version of `walletd`!
{% endhint %}
