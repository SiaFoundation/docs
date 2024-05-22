---
description: >-
  A step-by-step guide for setting up rclone with renterd for Windows, Mac OS,
  and Linux.
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

# rclone

## What is rclone?

Rclone is a command-line program to manage files on cloud storage. Rclone is very feature-rich and integrates with dozens of cloud storage providers, including any S3-compatible object stores like Sia `renterd`.

> Users call rclone _"The Swiss army knife of cloud storage"_, and _"Technology indistinguishable from magic"_.

Rclone [mounts](https://rclone.org/commands/rclone\_mount/) any local, cloud, or virtual filesystem as a disk on Windows, Mac OS, Linux, and FreeBSD and serves these over [SFTP](https://rclone.org/commands/rclone\_serve\_sftp/), [HTTP](https://rclone.org/commands/rclone\_serve\_http/), [WebDAV](https://rclone.org/commands/rclone\_serve\_webdav/), [FTP](https://rclone.org/commands/rclone\_serve\_ftp/), and [DLNA](https://rclone.org/commands/rclone\_serve\_dlna/). The mount lets us interact with our Sia `renterd` storage as a regular filesystem. We can mount `renterd` storage to a server’s filesystem or even a local laptop’s filesystem.

## Step 1: Install `renterd` and configure S3
This guide requires that you have a working installation of `renterd`. If you have not already installed `renterd`, you will need to do so before continuing.

{% hint style="warning" %}
Make sure to configure S3 when installing `renterd`, as this will be required later.
{% endhint %}

{% embed url="https://docs.sia.tech/renting/setting-up-renterd/" %}

## Step 2: Install `rclone`

{% hint style="danger" %}
Please note that only `rclone` versions 1.56.0 and above are supported.
{% endhint %}

Install `rclone` for your system using the official [`rclone` install guide](https://rclone.org/install/).

{% embed url="https://rclone.org/install/" %}

## Step 3: Configuring `rclone`

Now `rclone` has been installed, you can use the interactive configuration wizard to set up a new remote. To do so, run the following command from the Terminal.

```shell-session
rclone config
```

When the configuration wizard loads, enter `n` to create a new remote.

```shell-session
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
```

Next, name your remote. You can name it anything you want, but for this guide, we will be naming it `renterd`.

```shell-session
Enter name for new remote.
name> renterd
```

You will now be given a list of `Storage` options. Type in `s3` and press `Enter`.

```shell-session
Option Storage.
Type of storage to configure.
Choose a number from below, or type in your own value.
...
Storage> s3
```

Next, you will be asked to select a `Provider`. Type in `other` and press `Enter`

```shell-session
Option provider.
Choose your S3 provider.
Choose a number from below, or type in your own value.
...
provider> Other
```

You will now be asked to select how you would like to supply your S3 credentials. Since we are supplying an `access_key_id` and `secret_access_key`, we will not be using environment variables. Type in `false` or simply press `Enter` to use the default.

```shell-session
Option env_auth.
Get AWS credentials from runtime (environment variables or EC2/ECS meta data if no env vars).
Only applies if access_key_id and secret_access_key is blank.
Choose a number from below, or type in your own boolean value (true or false).
Press Enter for the default (false).
...
env_auth> false
```

For the next two questions, you will be prompted for your `access_key_id` and `secret_access_key` that you set in [Step 1](rclone.md#step-1-enable-renterd-s3-api).

```shell-session
Option access_key_id.
AWS Access Key ID.
Leave blank for anonymous access or runtime credentials.
Enter a value. Press Enter to leave empty.
access_key_id> your_renterd_access_key
```

```shell-session
Option secret_access_key.
AWS Secret Access Key (password).
Leave blank for anonymous access or runtime credentials.
Enter a value. Press Enter to leave empty.
secret_access_key> your_renterd_secret_key
```

When prompted for your `Region`, press `Enter` to leave it blank.

```shell-session
Option region.
Region to connect to.
Leave blank if you are using an S3 clone and you don't have a region.
Choose a number from below, or type in your own value.
Press Enter to leave empty.
...
region>
```

You will now be asked to enter an `Endpoint`. This should be the same as the `address` parameter we configured in our `renterd.yml` for [Step 1](rclone.md#step-1-enable-renterd-s3-api).

```shell-session
Option endpoint.
Endpoint for S3 API.
Required when using an S3 clone.
Enter a value. Press Enter to leave empty.
endpoint> http://localhost:8080
```

When asked for a `Location constraint` press `Enter` to leave it empty.

```shell-session
Option location_constraint.
Location constraint - must be set to match the Region.
Leave blank if not sure. Used when creating buckets only.
Enter a value. Press Enter to leave empty.
location_constraint>
```

Next, you will be asked to select an `ACL` from the list provided. Type in `private` and press `Enter`.

```shell-session
Option acl.
Canned ACL used when creating buckets and storing or copying objects.
This ACL is used for creating objects and if bucket_acl isn't set, for creating buckets too.
For more info visit https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl
Note that this ACL is applied when server-side copying objects as S3
doesn't copy the ACL from the source but rather writes a fresh one.
If the acl is an empty string then no X-Amz-Acl: header is added and
the default (private) will be used.
Choose a number from below, or type in your own value.
Press Enter to leave empty.
...
acl> private
```

When asked if you would like to edit the advanced config, type in `n` and press `Enter`.

```shell-session
Edit advanced config?
y) Yes
n) No (default)
y/n> n
```

You will now be given a summary of your new remote. If they are correct, you can type in `y` and press `Enter` to save your remote.

```shell-session
Configuration complete.
Options:
- type: s3
- provider: other
- access_key_id: your_renterd_access_key
- secret_access_key: your_renterd_secret_key
- endpoint: localhost:8080
- acl: private
Keep this "renterd" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

You have now successfully created a remote for `renterd`. You can now type in `q` and press `Enter` to quit the configuration wizard.

## Step 4: Mount the filesystem

Now that your `renterd` remote has been configured, it can be mounted on your computer's filesystem.

```shell-session
rclone mount renterd:/default /path/to/mount/point/ --s3-chunk-size 120MiB --fast-list --vfs-cache-mode full --daemon
```

{% hint style="info" %}

{% endhint %}

## All done.

{% hint style="success" %}
`renterd` should now be successfully mounted on your computer's filesystem. For more details and system-specific instructions, visit the official [`rclone` documentation](https://rclone.org/commands/rclone_mount/)

{% embed url="https://rclone.org/commands/rclone_mount/" %}
{% endhint %}
