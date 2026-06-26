---
description: Run indexd and PostgreSQL together using Docker Compose
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

This guide will walk you through setting up `indexd` using Docker Compose. Because `indexd` requires a PostgreSQL database, this is the **recommended** way to self-host: Docker Compose runs `indexd` and PostgreSQL together, so you don't have to install or manage a database separately.

{% hint style="success" %}
If you just want to store files, you don't need to run `indexd` at all — [Sia Storage](https://sia.storage) gives you 50 GB free with nothing to run.
{% endhint %}

---

## Pre-requisites

* **Software Requirements:** Before installing `indexd`, you will need to install [Docker](https://www.docker.com/get-started/).

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended.
  - A quad-core CPU
  - 8GB of RAM
  - 256 GB SSD for `indexd` and its PostgreSQL database

* **Network Access:** `indexd` interacts with the Sia network, so you need a stable internet connection and open network access to connect to the Sia blockchain.

{% hint style="info" %}
PostgreSQL is provided automatically by the Compose file below, so you do **not** need to install it yourself for this method.
{% endhint %}

## Create the compose file

Create a new file named `docker-compose.yml`. You can use the following as a template. The `postgres` service stores the `indexd` index, and the `indexd-data` volume holds the consensus data and config file.

```yml
services:
  postgres:
    image: postgres:18
    restart: unless-stopped
    shm_size: 128mb
    environment:
      POSTGRES_USER: indexd
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: indexd
    volumes:
      - postgres:/var/lib/postgresql
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $${POSTGRES_USER} -d $${POSTGRES_DB}"]
      interval: 5s
      timeout: 5s
      retries: 10
      start_period: 10s

  indexd:
    depends_on:
      postgres:
        condition: service_healthy
    image: ghcr.io/siafoundation/indexd:latest
    restart: unless-stopped
    ports:
      - 127.0.0.1:9980:9980/tcp # admin UI and API (kept local)
      - 9981:9981/tcp # public syncer
      - 9982:9982/tcp # public application API
    volumes:
      - indexd-data:/data

volumes:
  indexd-data:
  postgres:
```

{% hint style="warning" %}
Be careful with port 9980 (the admin UI and API) as Docker will expose it publicly by default. It is recommended to bind it to `127.0.0.1` to prevent unauthorized access. Ports 9981 (syncer) and 9982 (application API) are meant to be reachable by the network and your applications.
{% endhint %}

## Set the database password

Create a file named `.env` in the same directory as your `docker-compose.yml` and set a password for the PostgreSQL database:

```sh
POSTGRES_PASSWORD=your-secure-database-password
```

You will enter this same password during the `indexd` configuration step so the indexer can connect to the database.

## Getting the `indexd` image

To get the latest `indexd` image run the following command:
```console
docker compose pull
```

![](../../.gitbook/assets/indexd-screenshots/install/docker/01-indexd-docker-pull.png)

## Generate a recovery phrase

`indexd` uses a wallet to pay for storage contracts. If you don't already have a recovery phrase, generate one:

```console
docker compose run --rm indexd seed
```

{% hint style="warning" %}
Write your recovery phrase down and store it somewhere safe. It controls the wallet that funds your contracts and cannot be recovered if lost.
{% endhint %}

## Configuring `indexd`

Now launch the interactive configuration wizard:

```console
docker compose run --rm -it indexd config
```

The wizard will ask you for:

* Your **wallet recovery phrase** (use the one you generated above).
* An **admin password** used to unlock the `indexd` admin UI.
* A **database password** — enter the same value you set in `.env`.
* An **application API advertise URL** — the public URL applications will use to reach this indexer.

When asked whether to configure **advanced settings**, answer `yes` and set the database connection so `indexd` can reach the PostgreSQL container:

| Setting | Value |
|---------|-------|
| Database address | `postgres:5432` |
| Database user | `indexd` |
| Database name | `indexd` |
| SSL mode | `disable` |

![](../../.gitbook/assets/indexd-screenshots/install/docker/02-indexd-docker-config.png)

## Running `indexd`

Now that you have `indexd` configured, start the services:

```console
docker compose up -d
```

![](../../.gitbook/assets/indexd-screenshots/install/docker/03-indexd-docker-started.png)

Once `indexd` has successfully started, you can access the admin UI by opening your browser and going to [http://localhost:9980](http://localhost:9980/).

![](../../.gitbook/assets/indexd-screenshots/indexd-ui.png)

{% hint style="success" %}
Congratulations, you have successfully set up `indexd`.
{% endhint %}

## Fund your wallet

`indexd` uses a built-in wallet to pay storage providers for the contracts it forms on your behalf, so it needs Siacoin (SC) before it can store any data. After signing in, the **Welcome to Sia** checklist in the admin UI walks you through the remaining setup, including funding your wallet.

Open the **Wallet** section of the UI, copy your receiving address, and send Siacoin to it from an exchange or another wallet. See [Transferring Siacoins](../transferring-siacoins.md) for the full send and receive flow.

Once your wallet shows a confirmed balance, `indexd` can begin forming contracts and storing data.

## Checking the container status

To check the status of the containers run:
```console
docker compose ps
```

## Checking the logs

To check the `indexd` logs run:
```console
docker compose logs indexd
```

## Upgrading `indexd`

New versions of `indexd` are released regularly and contain bug fixes and performance improvements. To upgrade to the newest version, run the following:

```console
docker compose pull && docker compose up -d
```

{% hint style="success" %}
Congratulations, you have successfully updated your version of `indexd`!
{% endhint %}
