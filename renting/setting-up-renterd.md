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
# Setting up renterd

{% tabs %}
{% tab title="Windows" %}
# Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

### **Network Access:**
`renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

### **Operating System Compatibility:**
`renterd` is only compatible with Windows 64bit systems.

### **Hardware Requirements:**
A stable setup that meets the following specifications is recommended. Not meeting these requirements may result in preventing slabs from uploading and can lead to a loss of data.

- A dual-core CPU
- 16GB of RAM
- An SSD with at least 128GB of free space.

{% hint style="warning" %}
To ensure proper functionality, we are recommending 16GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
{% endhint %}

---

# Installing `renterd`

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

---

# Creating a wallet

`renterd` uses BIP-39 12-word recovery phrases. To generate a new wallet recovery phrase, run the following command:

```powershell
cd $HOME\sia\renterd\; `
.\renterd.exe seed
```

{% hint style="warning" %}
A new 12-word recovery phrase will be generated. Make sure to store it in a safe place, as you will need this phrase to recover your wallet.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/windows/03-renterd-seed.png)

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
  address: "localhost:9885"
  keypairsV4:
    your_access_key: your_private_key
```

Make sure to add your wallet seed and create an API password. The recovery phrase is the 12-word seed phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `renterd` web UI; it should be something secure and easy to remember.

{% hint style="warning" %}
`your_access_key` must be at least 16-characters long, and `your_private_key` must be at least 40-characters long.
{% endhint %}

Save your `renterd.yml` configuration using `ctrl+s` and close Notepad.

---

# Running `renterd`

Run the following command to start `renterd`.

```powershell
cd $HOME\sia\renterd; `
.\renterd.exe
```

![](../../.gitbook/assets/renterd-install-screenshots/windows/04-renterd-success.png)

You can now access the Sia network using the `renterd` web UI by opening a browser and going to [http://localhost:9980](http://localhost:9980/).

![](../../.gitbook/assets/renterd-install-screenshots/renterd-success.png)

Enter the API `password` you created in your `renterd.yml` to unlock the `renterd` web UI.

{% hint style="success" %}
Congratulations, you have successfully set up `renterd`.
{% endhint %}

---

# Updating `renterd`

To update `renterd` to the latest version, repeat the steps outlined in the [installation](#installing-renterd) section.
{% endtab %}

{% tab title="MacOS" %}
# Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

### **Network Access:**
`renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

### **Operating System Compatibility:**
You will need to ensure you download the correct `renterd` binary for your version of MacOS. To do this, click on the Apple icon in the top left corner of your toolbar, then click About This Mac. If the processor/chips says:


- **x86_64** — `MacOS AMD64`
- **M1, M2** — `MacOS ARM64`

### **Hardware Requirements:**
 A stable setup that meets the following specifications is recommended. 
Not meeting these requirements may result in preventing slabs from 
uploading and can lead to a loss of data.

- A dual-core CPU
- 16GB of RAM
- An SSD with at least 128GB of free space.

{% hint style="warning" %}
To ensure proper functionality, we are recommending 16GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
{% endhint%}

---

# Installing `renterd`

Press `CMD + Space` to open Spotlight search and open a `terminal`.

![](../../.gitbook/assets/renterd-install-screenshots/macos/00-renterd-run-terminal.png)

Once the Terminal loads, download and install `renterd` to your home folder.

{% hint style="warning" %}
Make sure to install the correct version for your system. If you are unsure which version you should pick, refer to the [Operating System Compatibility](#operating-system-compatibility-1) section of this guide for instructions.
{% endhint %}

- **Install `renterd` for `MacOS AMD64` systems:**

```
curl -O https://sia.tech/downloads/latest/renterd_darwin_amd64.zip
mkdir renterd &&\
unzip renterd_darwin_amd64.zip -d renterd &&\
rm -fr renterd_darwin_amd64.zip
```

- **Install `renterd` for `MacOS ARM64` systems:**

```
curl -O https://sia.tech/downloads/latest/renterd_darwin_arm64.zip
mkdir ~/renterd &&\
unzip renterd_darwin_arm64.zip -d ~/renterd &&\
rm -fr renterd_darwin_arm64.zip
```

![](../../.gitbook/assets/renterd-install-screenshots/macos/01-renterd-download-and-install.png)

---

# Creating a wallet

`renterd` uses BIP-39 12-word recovery phrases. To generate a new wallet recovery phrase, navigate to the `renterd` directory and run `renterd seed`:

```
cd ~/renterd && renterd seed
```

{% hint style="warning" %}
A new 12-word recovery phrase will be generated. Make sure to store it in a safe place, as you will need this phrase to recover your wallet.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/macos/02-renterd-seed.png)

Under your `renterd` directory create a new text document named `renterd.yml`.

```
nano ~/renterd/renterd.yml
```

Once the editor loads, enter the following and configure it as needed.

```
seed: your seed phrase goes here
http:
  password: your_api_password
autopilot:
  heartbeat: 5m
s3:
  enabled: true
  disableAuth: false
  address: "localhost:9885"
  keypairsV4:
    your_access_key: your_private_key
```

Make sure to add your wallet seed and create an API password. The recovery phrase is the 12-word seed phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `renterd` web UI; it should be something secure and easy to remember.

{% hint style="warning" %}
`your_access_key` must be at least 16-characters long, and `your_private_key` must be at least 40-characters long.
{% endhint %}

Save your `renterd.yml` configuration using `ctrl-o` and close the editor with `ctrl-x`.

---

# Running `renterd`

Run the following command to start `renterd`.

```
cd ~/renterd && ./renterd
```

![](../../.gitbook/assets/renterd-install-screenshots/macos/03-renterd-success.png)

You can now access the Sia network using the `renterd` web UI by opening a browser and going to [http://localhost:9880](http://localhost:9880/).

![](../../.gitbook/assets/renterd-install-screenshots/renterd-success.png)

Enter the API `password` you created in your `renterd.yml` to unlock the `renterd` web UI.

{% hint style="success" %}
Congratulations, you have successfully set up `renterd`.
{% endhint %}

# Updating `renterd`

To update `renterd` to the latest version, repeat the steps outlined in the [installation](#installing-renterd-1) section.
{% endtab %}

{% tab title="Linux" %}
# Pre-requisites

To ensure you will not run into any issues with running `renterd` it is recommended your system meets the following requirements:

### **Network Access:**
`renterd` needs a stable internet connection and open network access in order to store and retrieve data on the Sia network.

### **Operating System Compatibility:**
You must download the correct `renterd` binary for your version of Linux. If you are not sure which version you are on, you can run `uname -m` in a terminal to find out.

- **x86_64** — `Linux AMD64`
- **aarch64** — `Linux ARM64`

### **Hardware Requirements:**
 A stable setup that meets the following specifications is recommended. 
Not meeting these requirements may result in preventing slabs from 
uploading and can lead to a loss of data.

- A Linux distro with `systemd` (Ubuntu, Debian, Fedora, Arch, etc)
- A dual-core CPU
- 16GB of RAM
- An SSD with at least 128GB of free space.

{% hint style="warning" %}
To ensure proper functionality, we are recommending 16GB RAM. This is because `renterd` will keep full slabs in memory when uploading. A full slab is 120MB, and a single upload may hold two or three slabs in memory. However, it is possible to run `renterd` with less RAM than this, and it may work fine depending on the use case.
{% endhint %}

---

# Installing `renterd`

Open a Terminal using `Crtl + Alt + T`.

{% hint style="info" %}
If you cannot open a `Terminal` using the above method, try one of the other methods [listed here](https://www.geeksforgeeks.org/how-to-open-terminal-in-linux/).
{% endhint %}

Once the Terminal loads, run one of the following commands to download and install the latest version of `renterd` to your `/usr/local/bin` directory.

{% hint style="warning" %}
Make sure to install the correct version for your system. If you are unsure which version you should pick, refer to the [Operating System Compatibility](#operating-system-compatibility-2) section of this guide for instructions.
{% endhint %}

- **Install `renterd` for `Linux AMD64` systems:**

```
wget https://sia.tech/downloads/latest/renterd_linux_amd64.zip &&\
unzip -j renterd_linux_amd64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_amd64.zip
```

- **Install `renterd` for `Linux ARM64` systems:**

```
wget https://sia.tech/downloads/latest/renterd_linux_arm64.zip &&\
unzip -j renterd_linux_arm64.zip renterd &&\
sudo mv renterd /usr/local/bin/renterd &&\
rm -fr renterd_linux_arm64.zip
```

{% hint style="info" %}
You’ll be prompted to authorize this action by providing your system password. You will not see anything when you type this in. Press `Enter` once you have entered your password.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/linux/01-renterd-download-and-install.png)

---

# Creating a wallet

`renterd` uses BIP-39 12-word recovery phrases. To generate a new wallet recovery phrase, run the following command:

```
renterd seed
```

{% hint style="warning" %}
A new 12-word recovery phrase will be generated. Make sure to store it in a safe place, as you will need this phrase to recover your wallet.
{% endhint %}

![](../../.gitbook/assets/renterd-install-screenshots/linux/02-renterd-seed.png)

---

# Setting up a `systemd` service

Now that you have a recovery phrase, we will create a new system user and `systemd` service to run `renterd` securely on startup.

First, we will create a new system user with `useradd` and disable the creation of a home directory. This is a security precaution that will isolate `renterd` from any unauthorized access to our system. We will then use `usermod` to lock the account and prevent anyone from logging in under the account.

```
sudo useradd -M renterd &&\
sudo usermod -L renterd
```

Now, we will create a new folder under `/var/lib/` titled `renterd` and give it the appropriate permissions. This folder will be utilized specifically to store data related to the `renterd` software. Open the Terminal Emulator and run the following commands:

```
sudo mkdir /var/lib/renterd &&\
sudo chown renterd:renterd /var/lib/renterd &&\
sudo chmod o-rwx /var/lib/renterd
```

Next, create a file name `renterd.yml` file under `/var/lib/renterd/`

```
sudo nano /var/lib/renterd/renterd.yml
```

Now, modify the file to add your wallet seed and API password. The recovery phrase is the 12-word phrase you generated in the previous step. Type it carefully, with one space between each word, or copy it from the previous step. The password is used to unlock the `renterd` web UI; it should be something secure and easy to remember.

{% hint style="warning" %}
`your_access_key` must be at least 16-characters long, and `your_private_key` must be at least 40-characters long.
{% endhint %}

```
seed: your seed phrase goes here
http:
  password: your_api_password
autopilot:
  heartbeat: 5m
s3:
  enabled: true
  disableAuth: false
  address: "localhost:9885"
  keypairsV4:
    your_access_key: your_private_key
```

Once you have added your recovery phrase and password, save the file with `ctrl+s` and exit with `ctrl+x`.

Next, we’ll create a new system service to run `renterd` on startup:

```
sudo nano /etc/systemd/system/renterd.service
```

Once the editor loads, copy and paste the following into it.

```
[Unit]
Description=Sia renterd
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

You can now save the file with `ctrl+s` and exit with `ctrl+x`.

---

# Running `renterd`

Now it is time to start the service

```
sudo systemctl start renterd
```

Your `renterd` service should now be running. You can check the status of the service by running the following command:

```
sudo systemctl status renterd
```

If the service was set up correctly, it should say “active (running).”

![](../../.gitbook/assets/renterd-install-screenshots/linux/03-renterd-success.png)

You can now access the Sia network using the `renterd` web UI by opening a browser and going to [http://localhost:9880](http://localhost:9980/).

![](../../.gitbook/assets/renterd-install-screenshots/renterd-success.png)

Enter the API `password` you created in your `renterd.yml` to unlock the `renterd` web UI.

{% hint style="success" %}
Congratulations, you have successfully set up `renterd`.
{% endhint %}

---

# Updating `renterd`

To update `renterd` to the latest version, repeat the steps outlined in the [installation](#installing-renterd-2) section.
{% endtab %}
{% endtabs %}
