---
cover: https://sia.tech/assets/previews/renterd.png
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

# Windows

This guide will walk you through setting up `renterd` on Windows. At the end of this guide, you should have:

* Installed Sia `renterd` software
* Created a `renterd` wallet

## Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

* **Network Access:**
  `renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

* **Operating System Compatibility:**
  `renterd` is only compatible with Windows 64bit systems.

* **Hardware Requirements:**
  A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.

  - A dual-core CPU
  - 16GB of RAM
  - An SSD with at least 128GB of free space.

{% hint style="warning" %}
To ensure proper functionality, we are recommending 16GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
{% endhint %}

## Installing `renterd`

Press `windows key + R` to open the run dialog. Type in `powershell` and press `OK` to open a Terminal.

![](../../.gitbook/assets/renterd-install-screenshots/windows/00-renterd-run-powershell.png)

Once the Terminal loads, run the following command to download and install the latest version of `renterd`.

```powershell
wget https://sia.tech/downloads/latest/renterd_windows_amd64.zip -OutFile "$HOME\Downloads\renterd_windows_amd64.zip"; `
Expand-Archive "$HOME\Downloads\renterd_windows_amd64.zip" -DestinationPath "$HOME\sia\renterd"; `
Move-Item -Path "$HOME\sia\renterd\bin\renterd.exe" -Destination "$HOME\sia\renterd\renterd.exe" -Force; `
Remove-Item -LiteralPath "$HOME\sia\renterd\bin" -Recurse
```

{% hint style="warning" %}
When you paste multi-line commands into PowerShell, you will be prompted with a warning. Make sure you have copied the entire command and click `Paste anyway` to proceed.
{% endhint %}

![Click `Paste anyway` to proceed with installation.](../../.gitbook/assets/renterd-install-screenshots/windows/01-renterd-multiline-warn.png)

![Installation of renterd completed successfully.](../../.gitbook/assets/renterd-install-screenshots/windows/02-renterd-download-and-install.png)

## Creating a wallet

`renterd` uses BIP-39 12-word recovery phrases. To generate a new wallet recovery phrase, run the following command:

```powershell
cd $HOME\sia\renterd\; `
.\renterd.exe seed
```

{% hint style="warning" %}
A new 12-word recovery phrase will be generated. Make sure to store it in a safe place, as you will need this phrase to recover your wallet.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/windows/03-renterd-seed.png)

## Configure your `renterd.yml` file

Under `$HOME\sia\renterd\bin` create a new text document named `renterd.yml`.

```powershell
New-Item -Path "$HOME\sia\renterd" -Name "renterd.yml" -ItemType "file"; `
Start-Process "C:\WINDOWS\system32\notepad.exe" "$HOME\sia\renterd\renterd.yml"
```

Once Notepad loads, enter the following and configure it as needed.

```yaml
seed: your seed phrase goes here
http:
  password: your_api_password
autopilot:
  heartbeat: 5m
s3:
  enabled: true
  disableAuth: false
  address: "localhost:9985"
  keypairsV4:
    your_access_key: your_private_key
```

Make sure to add your wallet seed and create an API password. The recovery phrase is the 12-word seed phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `renterd` web UI; it should be something secure and easy to remember.

{% hint style="warning" %}
`your_access_key` can be anywhere from 16 to 128 characters long
`your_private_key` must be exactly 40 characters long.
{% endhint %}

Save your `renterd.yml` configuration using `ctrl+s` and close Notepad.

## Running `renterd`

Run the following command to start `renterd`.

```powershell
cd $HOME\sia\renterd; `
.\renterd.exe
```

{% hint style="warning" %}
Remember to leave the PowerShell open while `renterd` is running. If you close the command prompt window, `renterd` will stop.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/windows/04-renterd-success.png)

You can now access the Sia network using the `renterd` web UI by opening a browser and going to [http://localhost:9980](http://localhost:9980/).

![](../../.gitbook/assets/renterd-install-screenshots/renterd-success.png)

Enter the API `password` you created in your `renterd.yml` to unlock the `renterd` web UI.

{% hint style="success" %}
Congratulations, you have successfully set up `renterd`.
{% endhint %}

## Updating

New versions of `renterd` are released regularly and contain bug fixes and performance improvements.

To update:

1. Stop `renterd` if it is running. This can be accomplished by pressing `ctrl+c` in the PowerShell currently running `renterd`.

2. Download and install the latest version of `renterd`.

```powershell
wget https://sia.tech/downloads/latest/renterd_windows_amd64.zip -OutFile "$HOME\Downloads\renterd_windows_amd64.zip"; `
Expand-Archive "$HOME\Downloads\renterd_windows_amd64.zip" -DestinationPath "$HOME\sia\renterd"; `
Move-Item -Path "$HOME\sia\renterd\bin\renterd.exe" -Destination "$HOME\sia\renterd\renterd.exe" -Force; `
Remove-Item -LiteralPath "$HOME\sia\renterd\bin" -Recurse
```

3. Restart the `renterd` system service.
```powershell
cd $HOME\sia\renterd; `
.\renterd.exe
```

![Starting renterd](../../.gitbook/assets/renterd-install-screenshots/windows/04-renterd-success.png)

{% hint style="success" %}
Congratulations, you have successfully updated your version of `renterd`!
{% endhint %}
