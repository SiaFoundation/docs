---
description: This section takes you through setting up a host using Linux CLI
---

# Linux CLI

### Step 1: Install Sia binaries

{% hint style="warning" %}
_If you would like to use a different user account make sure to create it now before downloading and installing._
{% endhint %}

Download and extract the latest Sia Daemon Linux binaries from [https://sia.tech/get-started](https://sia.tech/get-started).

```
cd ~
wget -q https://sia.tech/releases/Sia-v1.5.7-linux-amd64.zip
unzip Sia-v1.5.7-linux-amd64.zip
```

Next move the extracted Sia binaries to `/usr/local/bin/`.

```
sudo mv -t /usr/local/bin Sia-v1.5.7-linux-amd64/siad Sia-v1.5.7-linux-amd64/siac
```



### Step 2: Configure Storage (Optional)

If you are using external drives, you will need to configure them to be mounted at boot.

To begin, locate the storage drive you would like to use for your renters data.

```
sudo fdisk -l
```

This will give a printout that looks similar to the following

```
Device         Boot  Start       End   Sectors   Size Id Type 
/dev/mmcblk0p1 *      2048    526335    524288   256M  c W95 FAT32 (LBA) 
/dev/mmcblk0p2      526336 250347486 249821151 119.1G 83 Linux 


Disk /dev/sda: 5.47 TiB, 6001175125504 bytes, 11721045167 sectors 
Disk model: Expansion Desk   
Units: sectors of 1 * 512 = 512 bytes 
Sector size (logical/physical): 512 bytes / 4096 bytes 
I/O size (minimum/optimal): 4096 bytes / 4096 bytes 
Disklabel type: gpt 
Disk identifier: 95C65D62-CA73-934A-9C4B-030C5FF0321F 


Device     Start         End     Sectors  Size Type 
/dev/sda1   2048 11721045133 11721043086  5.5T Linux filesystem
```

{% hint style="info" %}
_For this guide we will be using the 5.5TiB storage drive listed as_ `/dev/sda`
{% endhint %}

{% hint style="danger" %}
_This guide has been written assuming you have already formatted your storage device with the correct file system. If you have not done this already,_ [_please do so now_](../host-setup/advanced/formatting-storage.md#linux-cli)_._
{% endhint %}

Now you will also need to get the unique `UUID` for the device you'd like to use. To do this run the following.

```
sudo blkid
```

This will give you a print out similar to the following.

```
sudo blkid
[sudo] password for sia: 
/dev/sdb1: UUID="4c95307e-ecdf-4376-bf6b-1ad006e6144b" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="Linux filesystem" PARTUUID="33f86d9c-8f52-4202-9bf9-4c83c76239e4"
```

Once you have your devices `UUID`, you'll then need to create a new mount point.

```
sudo mkdir /mnt/SiaStorage01
```

Now all that is left is to update the `/etc/fstab` with your new mount point so it can be mounted on boot.

To do this first open up your `fstab` in a text editor.

```
sudo nano /etc/fstab
```

Once the editor loads you will need to add the following on a new line at the bottom of the file.

* UUID: The device UUID of the drive which should be mounted
* mount-point: The directory where the contents of the drive can be accessed from
* fs-type: The type of the file system
* options: Various mounting options, we use defaults which should be fine in most cases. Read more in what mount options can be used [here](https://en.wikipedia.org/wiki/Fstab).
* dump: Number telling the system how often the drive should be backed up.
* pass: Number indicated in which order (and if) fsck should check your device at boot 0 to avoid checking 1 if this is the root file system 2 if this is any other device.

```
UUID="4c95307e-ecdf-4376-bf6b-1ad006e6144b" /mnt/SiaStorage01 ext4 defaults 0 0
```

Save the file to disk using `ctrl+o`

Exit the text editor using `ctrl+x`



You can now verify it is working correctly by mounting the drive using the following.

```
sudo mount -a
```



### Step 3: Configure Services

In order for your host to automatically start up on reboot, you will need to create a new system service.

To begin, you will need to create a systemd script to run `siad` and login automatically at start up.

```
sudo nano /etc/systemd/system/siad.service
```

Once the text editor loads, copy and paste the following.

```
[Unit]
Description=Sia Daemon System Service
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/siad -M gctwh -d /home/ubuntu/siad
ExecStop=/usr/local/bin/siac stop
Restart=always
RestartSec=15
User=ubuntu
Environment=”SIA_WALLET_PASSWORD=walletseedphrase”
LimitNOFILE=900000

[Install]
WantedBy=multi-user.target
Alias=siad.service
```

{% hint style="warning" %}
If you are installing under a different user other than `ubuntu` make sure to update the `ExecStart` and `User` variables with the correct username.
{% endhint %}

Save the file to disk using `ctrl+o`

Exit the text editor using `ctrl+x`



To finish, run your new services and enable them to run at start up.

```
sudo systemctl start siad
sudo systemctl enable siad
```



### Step 4: Create a wallet

```
siac wallet init -p 
```

{% hint style="warning" %}
_Make sure to go back and replace the_ [_Environment variable in the service script you created in Step 3_](linux-cli.md#step-3-configure-services)_. You will need to replace `walletseedphrase` with your new seed._
{% endhint %}

{% hint style="danger" %}
_Write down your recovery keys and keep them somewhere safe. If you loose these you will not be able to recover your Siacoin._
{% endhint %}

Once created you'll then need to unlock the wallet using the seed phrase you wrote down.

```
siac wallet unlock
```



### Step 5: Fund your wallet

Generate a new wallet.

```
siac wallet address
```

Now that you have an address, you can send Siacoin to fund your wallet.

{% hint style="info" %}
_You can fund your wallet before your host has finished syncing to the blockchain. But you will not be able to see your funds until you have fully synced._
{% endhint %}

{% hint style="info" %}
_It is recommended to have about 1000 Siacoin per TB._
{% endhint %}



### Step 6: Host Settings

Set your minimum storage price.

{% hint style="info" %}
__[_Filebase_](../../layer-2-solutions/filebase/) _will only make contracts with hosts that have a storage price of 150SC or higher. Also_ [_Skynet Labs_](../../layer-2-solutions/skynet.md) _will not make contracts with hosts that have a storage price of 300SC or higher. Set your prices accordingly._
{% endhint %}

```
siac host config minstorageprice 150SC
```

Set your collateral.

{% hint style="warning" %}
_Your collateral should be two times your storage price. So if your storage price is set to 150SC, your collateral should be set to 300SC_
{% endhint %}

```
siac host config collateral 300SC
```

Set your bandwidth fees.

```
siac host config mindownloadbandwidthprice 250SC
siac host config minuploadbandwidthprice 50SC
```

Set your max contract length.

{% hint style="warning" %}
_The recommended minimum contract length is 12 weeks. Default is 26 weeks._
{% endhint %}

```
siac host config maxduration 12w
```

To see more configuration settings use the following.

```
siac host config -h
```



### Step 7: Bootstrapping

{% hint style="danger" %}
_Before you can begin hosting, you will need to wait for your host to be fully synced with the blockchain._
{% endhint %}

To monitor your bootstrap progress use the following.

```
siac consensus
```



### Step 8: Announce

Once you have completed syncing to the blockchain The only thing left, is for you to announce your host to the network.

```
siac host announce
```

#### If you signed up for a DDNS service

You need to announce your host using your DDNS hostname in order for it to work. You can also announce a specific IP address.

```
host announce example.ddns.net:9982
```

{% hint style="danger" %}
_Make sure to include_ `:9982` _as this specifies which port renters can contact you through and is the default for Sia._
{% endhint %}

{% hint style="info" %}
_Announcing your host is a transaction that will appear in your Transaction list in your wallet._
{% endhint %}



### Step 9: Retire

{% hint style="danger" %}
_Before retiring your host, you will first need to stop accepting contract and allow any current contracts to expire. Once all your remaining contracts have expired, you can then shut down your host without any loss of data or collateral._
{% endhint %}

```
siac host config acceptingcontracts false
```
