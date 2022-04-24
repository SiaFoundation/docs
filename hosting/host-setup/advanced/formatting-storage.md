---
description: This section will guide you through formatting a storage device.
---

# Formatting Storage

Choose your hosts operating system from below:

* [Linux](formatting-storage.md#linux-cli)

## Linux CLI

### Step 1: Locate Device

To begin, locate the storage you would like to format.

```
sudo fdisk -l
```

This will give a printout that looks similar to the following.

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
_This guide has been written assuming that you are intending to reformat the entire device. If there is any data already on the device, you should back it up now. **All data will be lost!**_
{% endhint %}



### Step 2: Delete Partitions

Once you have the location of your device, use `gdisk` to remove any existing partitions.

```
sudo gdisk /dev/sda
```

Once `gdisk` is open you should see something that looks similar to this.

```
GPT fdisk (gdisk) version 1.0.5

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
```

Enter `d` to delete a partition. When prompted enter the partition number you would like to delete.

```
Command (? for help): d
Partition number (1-2): 1
```

Repeat this process until you have removed all existing partitions.

Once that is done, you can then enter `w` to write the new partition to disk.

```
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING PARTITIONS!!

Do you want to proceed? (Y/N): Y
```



### Step 3: Create New Partition

Now that you have removed any existing partitions, you will need to create a new one.

Start by running `gdisk` again.

```
sudo gdisk /dev/sda
GPT fdisk (gdisk) version 1.0.5

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
```

Once `gdisk` has loaded, create a new partition by entering `n`, followed by the number `1`.

```
Command (? for help): n
Partition number (1-128, default 1): 1
```

Agree to any further prompts using the `enter` key.

```
First sector (34-11721045134, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-11721045134, default = 11721045134) or {+-}size{KMGTP}:
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
```

Once you have created your new partition, enter `w` to write these changes to disk and `y` to confirm.

```
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING PARTITIONS!!

Do you want to proceed? (Y/N): Y
OK; writing new GUID partition table (GPT) to /dev/sda.
The operation has completed successfully.
```



### Step 4: Format Partition

Now all that is left is for you to format your newly created partition.

```
sudo mkfs.ext4 /dev/sda1
```



Congratulations! [Your device is now ready to be added to your hosts storage](../../hosting-guides/linux-cli.md#step-2-configure-storage-optional).
