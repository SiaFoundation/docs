---
description: >-
  A step-by-step guide for configuring a reverse proxy with Caddy.
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

# Caddy Webserver

## What is `Caddy`?

Caddy is a powerful, extensible platform used to serve web content securely over HTTPS. This guide will teach you how to install and configure Caddy to create an HTTPS connection to the `renterd` S3 API using your custom domain name.

## Why a reverse proxy?

A reverse proxy is a server that sits in front of one or more web servers, redirecting client requests to these servers and returning the responses to the clients. This setup enhances security, load balancing, and performance. When used with `renterd` integrations, a reverse proxy like `Caddy` can securely manage `HTTPS` connections, effectively hiding the backend server details, offering encrypted communication, and simplifying SSL certificate management, making remote connections to `renterd` integrations more secure and efficient.

## **Pre-Requisites**

- A registered domain name with a DNS `A` record pointing to your server’s IP address.

## Step 1: Download and install Caddy

{% tabs %}
{% tab title="Windows" %}

```console
curl.exe https://webi.ms/caddy | powershell
```

{% endtab %}
{% tab title="macOS" %}

```console
curl -sS https://webi.sh/caddy | sh
```

{% endtab %}
{% tab title="Linux" %}

```console
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```
{% endtab %}
{% endtabs %}

Caddy should now be running. To double-check that it is, you can use the following command:

{% tabs %}
{% tab title="Windows" %}
Windows
{% endtab %}
{% tab title="macOS" %}
macOS
{% endtab %}
{% tab title="Linux" %}

```console
sudo systemctl status caddy
```

If Caddy is not running, use the following command to start the service and enable it to run on startup:

```console
sudo systemctl enable --now caddy
sudo systemctl start caddy
```
{% endtab %}
{% endtabs %}

## Step 2: Configure `Caddyfile`

Now that Caddy is running as a service. We will edit our `Caddyfile` and configure a `reverse_proxy` using our domain name.

{% tabs %}
{% tab title="Windows" %}

{% endtab %}
{% tab title="macOS" %}

{% endtab %}
{% tab title="Linux" %}
```console
sudo nano /etc/caddy/Caddyfile
```
{% endtab %}
{% endtabs %}

Once the editor loads, add the following and replace `your.domain.com` with your actual domain name.

```console
your.domain.com {
    reverse_proxy http://localhost:9985
}
```

{% hint style=”info” %}
The `reverse_proxy` directive is set to `http://localhost:9885`, directing traffic to the `renterd` S3 API running locally on port 9985.
{% endhint %}

Once you have finished, save your `Caddyfile` and exit the editor. Then, run the following command to apply the new configuration.

{% hint style="info" %}
For more detailed Caddy configurations, visit our [Sia Starter Examples Repository](https://github.com/SiaFoundation/sia-starter-examples/)
{% endhint %}

{% tabs %}
{% tab title="Windows" %}

{% endtab %}
{% tab title="macOS" %}

{% endtab %}
{% tab title="Linux" %}
```console
caddy reload
```
{% endtab %}
{% endtabs %}

## All Done.

Congratulations! Now that you have successfully installed and configured Caddy, you can connect to your device securely over `HTTPS`.