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

**TODO: Install without apt**

# Linux

This guide will walk you through setting up `renterd` on Linux. At the end of this guide, you should have the following:

* Installed Sia `renterd` software
* Created a `renterd` wallet

---

## Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

* **Network Access:** `renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

* **Operating System Compatibility:** You must download the correct `renterd` binary for your version of Linux. If you are not sure which version you are on, you can run `uname -m` in a terminal to find out.
  - **x86_64** — `Linux AMD64`
  - **aarch64** — `Linux ARM64`

* **System Updates:** Ensure that your Linux is up to date with the latest system updates, as these updates can contain important security fixes and improvements.

* **Hardware Requirements:** A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.
  - A Linux distro with `systemd` (Ubuntu, Debian, Fedora, Arch, etc)
  - A dual-core CPU
  - 16GB of RAM
  - An SSD with at least 128GB of free space.

  {% hint style="warning" %}
  To ensure proper functionality, we are recommending 16GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
  {% endhint %}

---

## Installing `renterd`

Open a Terminal using `Crtl + Alt + T`.

{% hint style="info" %}
If you cannot open a `Terminal` using the above method, try one of the other methods [listed here](https://www.geeksforgeeks.org/how-to-open-terminal-in-linux/).
{% endhint %}

Once the Terminal loads, run one of the following commands to download and install the latest version of `renterd` to your `/usr/local/bin` directory.

{% hint style="warning" %}
Make sure to install the correct version for your system. If you are unsure which version you should pick, refer to the [Pre-requisites](#pre-requisites) section of this guide for instructions.
{% endhint %}

{% tabs %}
{% tab title="AMD64" %}
```console
wget https://sia.tech/downloads/latest/renterd_linux_amd64.zip &&\
unzip -j renterd_linux_amd64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_linux_arm64.zip &&\
unzip -j renterd_linux_arm64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_arm64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_amd64.zip &&\
unzip -j renterd_zen_linux_amd64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd_zen &&\
rm -fr renterd_zen_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_arm64.zip &&\
unzip -j renterd_zen_linux_arm64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd_zen &&\
rm -fr renterd_zen_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You’ll be prompted to authorize this action by providing your system password. You will not see anything when you type this in. Press `Enter` once you have entered your password.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/linux/01-renterd-download-and-install.png)

---

## Creating a wallet

`renterd` uses BIP-39 12-word recovery phrases. To generate a new wallet recovery phrase, run the following command:

{% tabs %}
{% tab title="Mainnet" %}
```console
renterd seed
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
renterd_zen seed
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
A new 12-word recovery phrase will be generated. Make sure to store it in a safe place, as you will need this phrase to recover your wallet.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/linux/debian/01-renterd-debian-apt-install.png)

---

## Setting up a system user

Now that you have a recovery phrase, we will create a new system user and `systemd` service to run `renterd` securely on startup.

First, we will create a new system user with `useradd` and disable the creation of a home directory. This is a security precaution that will isolate `renterd` from any unauthorized access to our system. We will then use `usermod` to lock the account and prevent anyone from logging in under the account.

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo useradd -M renterd &&\
sudo usermod -L renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo useradd -M renterd_zen &&\
sudo usermod -L renterd_zen
```
{% endtab %}
{% endtabs %}

Now, we will create a new folder under `/var/lib/` titled `renterd` and give it the appropriate permissions. This folder will be utilized specifically to store data related to the `renterd` software. Open the Terminal Emulator and run the following commands:

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo mkdir /var/lib/renterd &&\
sudo chown renterd:renterd /var/lib/renterd &&\
sudo chmod o-rwx /var/lib/renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo mkdir /var/lib/renterd_zen &&\
sudo chown renterd_zen:renterd_zen /var/lib/renterd_zen &&\
sudo chmod o-rwx /var/lib/renterd_zen
```
{% endtab %}
{% endtabs %}

---

## Configure your `renterd.yml` file

To begin, create a file name `renterd.yml` file under `/var/lib/renterd/`

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo nano /var/lib/renterd/renterd.yml
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo nano /var/lib/renterd_zen/renterd.yml
```
{% endtab %}
{% endtabs %}

Now, modify the file to add your wallet seed and API password. The recovery phrase is the 12-word phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `renterd` web UI; it should be something secure and easy to remember.

{% hint style="warning" %}
`your_access_key` can be anywhere from 16 to 128 characters long, and `your_private_key` must be exactly 40 characters long.
{% endhint %}

```yaml
seed: your seed phrase goes here
http:
  password: your_api_password
autopilot:
  heartbeat: 5m
```

Once you have added your recovery phrase and password, save the file with `ctrl+s` and exit with `ctrl+x`.

---

## Setting up a systemd service

Now we can create a new system service to run `renterd` on startup:

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo nano /etc/systemd/system/renterd.service
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo nano /etc/systemd/system/renterd_zen.service
```
{% endtab %}
{% endtabs %}

Once the editor loads, copy and paste the following into it.

{% tabs %}
{% tab title="Mainnet" %}
```toml
[Unit]
Description=renterd
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/renterd
WorkingDirectory=/var/lib/renterd
Restart=always
RestartSec=15
User=renterd

[Install]
WantedBy=multi-user.target
Alias=renterd.service
```
{% endtab %}

{% tab title="Zen Testnet" %}
```toml
[Unit]
Description=renterd (Zen Testnet)
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/renterd_zen
WorkingDirectory=/var/lib/renterd_zen
Restart=always
RestartSec=15
User=renterd_zen

[Install]
WantedBy=multi-user.target
Alias=renterd_zen.service
```
{% endtab %}
{% endtabs %}

You can now save the file with `ctrl+s` and exit with `ctrl+x`.

---

## Running `renterd`

Now it is time to start the service

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo systemctl start renterd &&\
sudo systemctl enable renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo systemctl start renterd_zen &&\
sudo systemctl enable renterd_zen
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
On newer versions of Linux (Ubuntu 22.04+), `sudo systemctl enable renterd` may not be required as the service will automatically be enabled by default. If you get an error saying the service failed to be enabled due to the file already existing, it is okay to ignore it.
{% endhint %}

Your `renterd` service should now be running. You can check the status of the service by running the following command:

{% tabs %}
{% tab title="Mainnet" %}
```console
sudo systemctl status renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo systemctl status renterd_zen
```
{% endtab %}
{% endtabs %}

If the service was set up correctly, it should say “active (running).”

{% hint style="warning" %}
If for some reason your `renterd` service will not start, use the command `journalctl -fu renterd` to view the console output for more information.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/linux/03-renterd-success.png)

You can now access the Sia network using the `renterd` web UI by opening a browser and going to [http://localhost:9980](http://localhost:9980/).

{% hint style="warning" %}
If you are running `renterd` on the Zen Testnet, you will need to access the web UI on port `9880` by going to [http://localhost:9880](http://localhost:9880).
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/renterd-success.png)

Enter the API `password` you created in your `renterd.yml` to unlock the `renterd` web UI.

{% hint style="success" %}
Congratulations, you have successfully set up `renterd`.
{% endhint %}

---

## Updating

New versions of `renterd` are released regularly and contain bug fixes and performance improvements.

**To update:**

1. Stop the `renterd` system service.
{% tabs %}
{% tab title="Mainnet" %}
```console
sudo systemctl stop renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo systemctl stop renterd_zen
```
{% endtab %}
{% endtabs %}

2. Download and install the latest version of `renterd`.

{% hint style="warning" %}
Make sure to install the correct version for your system. If you are unsure which version you should pick, refer to the [Pre-requisites](#pre-requisites) section of this guide for instructions.
{% endhint %}

{% tabs %}
{% tab title="AMD64" %}
```console
wget https://sia.tech/downloads/latest/renterd_linux_amd64.zip &&\
unzip -j renterd_linux_amd64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_amd64.zip
```
{% endtab %}

{% tab title="ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_linux_arm64.zip &&\
unzip -j renterd_linux_arm64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_arm64.zip
```
{% endtab %}

{% tab title="Zen AMD64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_amd64.zip &&\
unzip -j renterd_zen_linux_amd64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd_zen &&\
rm -fr renterd_zen_linux_amd64.zip
```
{% endtab %}

{% tab title="Zen ARM64" %}
```console
wget https://sia.tech/downloads/latest/renterd_zen_linux_arm64.zip &&\
unzip -j renterd_zen_linux_arm64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd_zen &&\
rm -fr renterd_zen_linux_arm64.zip
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You'll be prompted to authorize this action by providing your system password. Type this in and press enter to continue.
{% endhint %}

3. Restart the `renterd` system service.
{% tabs %}
{% tab title="Mainnet" %}
```console
sudo systemctl start renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo systemctl start renterd_zen
```
{% endtab %}
{% endtabs %}

4. Verify the `renterd` service is running correctly.
{% tabs %}
{% tab title="Mainnet" %}
```console
sudo systemctl status renterd
```
{% endtab %}

{% tab title="Zen Testnet" %}
```console
sudo systemctl status renterd_zen
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
If, for some reason, the `renterd` service will not start, use the command `journalctl -fu renterd` to view the console output for more information.
{% endhint %}

![Starting renterd](../../.gitbook/assets/renterd-success.png)

{% hint style="success" %}
Congratulations, you have successfully updated your version of `renterd`!
{% endhint %}
