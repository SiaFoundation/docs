---
description: Connect an application to a self-hosted indexd
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

# Connect an application

Applications connect to the **application API** using the advertise URL configured during setup. Before creating a connect key, confirm that this URL is reachable from the application and matches the public scheme, hostname, and port exactly.

For access from another device, put the application API behind an HTTPS reverse proxy and use that public HTTPS URL. Do not use the admin UI URL or expose the admin API on port `9980`. See [Choose the application API advertise URL](docker.md#choose-the-application-api-advertise-url) for configuration examples, common mistakes, and a connectivity check.

1. Sign in to the `indexd` admin UI and open **Connect keys**.
2. Select **Create key**, choose a quota, and create the key.
3. Copy the new key and keep it secret.
4. In the application, choose its custom or self-hosted indexer option and enter the advertise URL exactly as configured in `indexd`.
5. On the approval page opened by the application, paste the connect key into the **App password** field and select **Accept**.
6. Return to the application and enter the application's recovery phrase when prompted.

The connect key, `indexd` admin password, PostgreSQL password, application recovery phrase, and `indexd` wallet recovery phrase are separate credentials. Initial registration consumes one use from the connect key's quota; later requests are signed with the application's derived App Key.
