---
description: Run your own Sia indexer with indexd
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

# Setting up indexd

`indexd` is the Sia Foundation's indexer daemon. It is the component that **manages contracts** with storage providers, tracks where your objects live on the network, monitors their health, and repairs data in the background. Applications connect to an indexer (through a [Sia Storage SDK](../about-renting.md)) to store and retrieve data without managing hosts or contracts themselves.

{% hint style="success" %}
**Most people don't need to run `indexd`.** [Sia Storage](https://sia.storage) is a hosted service that gives you **50 GB free** with nothing to install, run, or maintain — no server, no database, and no contracts to manage. Use Sia Storage unless you specifically want to operate your own indexer.
{% endhint %}

## Who should self-host?

Most people, including developers building applications, should not run their own indexer. Point your application at [Sia Storage](https://sia.storage) during development instead. An application connects to a hosted indexer exactly the same way it connects to one you run yourself, so there is no need to operate one in order to build or test against it.

The only reason to run your own `indexd` is to retain full control over the infrastructure your data and contracts depend on, rather than relying on a hosted service. This is a decision an individual user makes for their own data, not one an application should make on their behalf.

## Before you start

`indexd` is a server daemon, not a desktop application:

* **There is no desktop app.** `indexd` is run from the command line or in a container.
* **PostgreSQL 18 is required.** `indexd` stores its index in a PostgreSQL database. The [Docker](docker.md) guide runs PostgreSQL for you in a second container, so you don't have to install or manage a database separately.

## Install

* [**Docker**](docker.md) — runs `indexd` and PostgreSQL together with Docker Compose. This is the recommended way to self-host.

{% hint style="info" %}
You can also run the `indexd` binary directly against your own PostgreSQL server. The binaries are available on the [official website](https://sia.tech/software/indexd), and configuration options are documented in the [indexd repository](https://github.com/SiaFoundation/indexd).
{% endhint %}

## Next steps

* Configure [**backups and recovery**](operations.md) before storing production data.
* [**Connect an application**](connect-application.md) using a connect key.
