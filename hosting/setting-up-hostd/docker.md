---
description: Setup a new host using Docker compose
cover: https://sia.tech/assets/previews/hostd.png
coverY: 0
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

# macOS

This guide will walk you through setting up `hostd` using Docker compose. At the end of this guide, you should have the following:

* Installed Sia `hostd` software
* Created a `hostd` wallet

---

## Pre-requisites

To ensure you will not run into any issues with running `hostd` it is recommended your system meets the following requirements:

* **Network Access:** `hostd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network. You will also need to forward the ports `9981-9984` so `hostd` can properly communicate with the network and renters.
* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.
  - A quad-core CPU
  - 8GB of RAM
  - An SSD with at least 128GB of free space.
* **Software Requirements:** Before installing `hostd`, you will need to install [Docker](https://www.docker.com/get-started/).

## Create the compose file

Create a new file named `docker-compose.yml`. You can use the following as a template. The `/data` mount is where consensus data is stored and is required. Change the `/storage` mount to the path of your storage drive. If you have additional storage disks, add them.

```yml
services:
  hostd:
    image: ghcr.io/siafoundation/hostd:latest
    restart: unless-stopped
    ports:
      - 127.0.0.1:9980:9980/tcp
      - 9981-9984:9981-9984/tcp
    volumes:
      - hostd-data:/data
      - /storage:/storage

volumes:
  hostd-data:
```

{% hint style="warning" %}Be careful with port 9980 as Docker will expose it publicly by default. It is recommended to bind it to 127.0.0.1 to prevent unauthorized access. If you need to expose it to a LAN, ensure the port is not accessible publicly.{% endhint %}

## Getting the `hostd` image

To get the latest `hostd` image run the following command:
```
docker compose pull
```

## Configuring `hostd`

Now that you have the latest `hostd` image downloaded, you will need to create a seed phrase and admin password. To launch the built-in configuration wizard, run the following:

```console
docker compose run --rm -it hostd config
```

![](../../.gitbook/assets/hostd-install-screenshots/docker/docker_hostd_config.gif)

When the configuration wizard loads, you will be asked to verify the location of your data directory. Type `no` to keep the default.

![](../../.gitbook/assets/hostd-install-screenshots/docker/01_docker_hostd_config.png)

Next, you will be asked to enter a seed phrase. If you already have one that you would like to use, you can enter it now. Otherwise, you can type `seed` to generate a new one. For the purpose of this guide, we will generate a new seed.

![](../../.gitbook/assets/hostd-install-screenshots/docker/02_docker_hostd_config.png)

Next, you will be prompted to enter an admin password. This is used to unlock the `hostd` web UI.

![](../../.gitbook/assets/hostd-install-screenshots/docker/03_docker_hostd_config.png)

Finally, you will be asked if you want to configure advanced settings for `hostd`. Type `no` and hit enter to exit the configuration wizard.

![](../../.gitbook/assets/hostd-install-screenshots/docker/04_docker_hostd_config.png)

## Running `hostd`

Now that you have `hostd` successfully installed and configured, it is time to run it. Use the following command to start `hostd`:

```console
docker compose up -d
```

![](../../.gitbook/assets/hostd-install-screenshots/macos/06-hostd-startup.png)

Once `hostd` has successfully started, you can access the web UI by opening your browser and going to [http://localhost:9980](http://localhost:9980/).

![](../../.gitbook/assets/hostd-install-screenshots/macos/07-hostd-webui.png)

{% hint style="success" %}
Congratulations, you have successfully set up `hostd`.
{% endhint %}

## Checking the container status

To check the status of the container run:
```
docker ps -a
```

If the container is not running, it will show in the `STATUS` column

![](../../.gitbook/assets/hostd-install-screenshots/docker/07_docker_hostd_status.png)

## Checking the logs

To check the container logs run:
```
docker compose logs hostd
```

![](../../.gitbook/assets/hostd-install-screenshots/docker/08_docker_hostd_logs.png)

## Upgrading `hostd`

It is essential to keep your host up to date. New versions of `hostd` are released regularly and contain bug fixes and performance improvements.

To upgrade your `hostd` to the newest version, make sure you have shut down `hostd` and then run the following:

```console
docker compose pull && docker compose up -d
```

{% hint style="success" %}
Congratulations, you have successfully updated your version of `hostd`!
{% endhint %}
