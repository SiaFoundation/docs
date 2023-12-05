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

{% hint style="warning" %}
This guide requires a working installation of `renterd`. If you have not already installed `renterd`, you will need to do so before continuing.

[**📖 `renterd` Installation Guide**](https://docs.sia.tech/v/current/renting/setting-up-renterd)
{% endhint %}

{% tabs %}
{% tab title="Windows" %}
For the purpose of this guide, we will start by uploading a file to the Sia Network using the `renterd` Web UI. This will be used later to help us verify we have configured things properly.

![A file uploaded to the Sia Network using `renterd`](../../.gitbook/assets/rclone-s3-integration/renterd-bucket.png)

***

## Step 1: Enable `renterd` S3 API

Before setting up `rclone`, we will need to enable `renterd`'s S3 interface if you have not done so already. This is done by editing your `renterd.yml` file. If you are unsure where your `renterd.yml` is installed, please refer to the correct [installation guide](https://docs.sia.tech/v/current/renting/setting-up-renterd) for your system.

Once you have located your `renterd.yml` file, open it with your preferred text editor and add the following:

```yaml
s3:
  enabled: true
  address: localhost:9985
  keypairsV4:
    your_renterd_access_key: your_renterd_secret_key
```

Make sure to replace `your_renterd_access_key` and `your_renterd_secret_key` with unique passphrases. They can be anything you want but must be at least 16 characters in length, and your secret key should always be kept private. Keep these values on hand. You will need them for Step 3.

{% hint style="warning" %}
If you are running `renterd` in a docker container, you will need to override the address via docker: `command: -s3.address:9985`
{% endhint %}



***

## Step 2: Install `rclone`

Press `windows key + R` to open the run dialog. Type in `powershell` and press `OK` to open a Terminal.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-win-01.png)

Once the Terminal loads, run the following command to install `rclone`.

```powershell
winget install Rclone.Rclone
```

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-win-02.png)

***

## Step 3: Configuring `rclone`

Now that we have `rclone` installed, we can use the interactive configuration wizard to set up a new remote. To do so, run the following command from the Terminal.

```shell-session
rclone config
```

{% hint style="info" %}
If the command does not work, you may need to restart your terminal first. To do so, close the current `Terminal` and use the same method you used above in [Step 2](rclone.md#step-2-install-rclone) to open a new one.
{% endhint %}

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
endpoint> http://localhost:9985
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
- endpoint: localhost:9985
- acl: private
Keep this "renterd" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

You have now successfully created a remote for `renterd`. You can now type in `q` and press `Enter` to quit the configuration wizard.



***

## Step 4: Mount the filesystem

Now that `renterd` is running and `rclone` is configured with `renterd` as a remote, we can mount the `renterd` storage to the filesystem.

{% hint style="warning" %}
Before you can use `rclone mount` on Windows, you will need to download and install [WinFsp](https://winfsp.dev/rel/).
{% endhint %}

Once you have installed `WinFsp`, you can then mount your `renterd` remote and assign it the drive letter `X:` using the following command.

```shell-session
rclone mount renterd:/default X: --vfs-cache-mode full
```

{% hint style="info" %}
On Windows, you can run `rclone mount` in the foreground only. The `--daemon` flag is ignored if used.
{% endhint %}

If you have configured everything properly, you should see a confirmation that `rclone` has successfully started.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-win-03.png)

To confirm you have mounted your Sia storage correctly, you should see a new `X:` drive on your filesystem.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-win-04.png)

You can now access your files on Sia directly from your File Explorer.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-win-05.png)
{% endtab %}

{% tab title="Mac OS" %}
For the purpose of this guide, we will start by uploading a file to the Sia Network using the `renterd` Web UI. This will be used later to help us verify we have configured things properly.

![A file uploaded to the Sia Network using `renterd`](../../.gitbook/assets/rclone-s3-integration/renterd-bucket.png)

***

## Step 1: Enable `renterd` S3 API

Before setting up `rclone`, we will need to enable `renterd`'s S3 interface if you have not done so already. This is done by editing your `renterd.yml` file. If you are unsure where your `renterd.yml` is installed, please refer to the correct [installation guide](https://docs.sia.tech/v/current/renting/setting-up-renterd) for your system.

Once you have located your `renterd.yml` file, open it with your preferred text editor and add the following:

```yaml
s3:
  enabled: true
  address: localhost:9985
  keypairsV4:
    your_renterd_access_key: your_renterd_secret_key
```

Make sure to replace `your_renterd_access_key` and `your_renterd_secret_key` with unique passphrases. They can be anything you want but must be at least 16 characters in length, and your secret key should always be kept private. Keep these values on hand. You will need them for Step 3.

{% hint style="warning" %}
If you are running `renterd` in a docker container, you will need to override the address via docker: `command: -s3.address:9985`
{% endhint %}

&#x20;

***

## Step 2: Install rclone

Press `CMD + Space` to open Spotlight search and open a `terminal`.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-01.png)

Once the Terminal loads, run the following command to install `rclone`.

{% code fullWidth="false" %}
```shell-session
sudo -v ; curl https://rclone.org/install.sh | sudo bash
```
{% endcode %}

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-02.png)

***

## Step 3: Configuring rclone

Now that we have `rclone` installed, we can use the interactive configuration wizard to set up a new remote. To do so, run the following command from the Terminal.

```shell-session
rclone config
```

{% hint style="info" %}
If the command does not work, you may need to restart your terminal first. To do so, close the current `Terminal` and use the same method you used above in [Step 2](rclone.md#step-2-install-rclone-1) to open a new one.
{% endhint %}

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

For the next two questions, you will be prompted for your `access_key_id` and `secret_access_key` that you set in [Step 1](rclone.md#step-1-enable-renterd-s3-api-1).

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

You will now be asked to enter an `Endpoint`. This should be the same as the `address` parameter we configured in our `renterd.yml` for [Step 1](rclone.md#step-1-enable-renterd-s3-api-1).

```shell-session
Option endpoint.
Endpoint for S3 API.
Required when using an S3 clone.
Enter a value. Press Enter to leave empty.
endpoint> http://localhost:9985
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
- endpoint: localhost:9985
- acl: private
Keep this "renterd" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

You have now successfully created a remote for `renterd`. You can now type in `q` and press `Enter` to quit the configuration wizard.



***

## Step 4: Mount the filesystem

Now that `renterd` is running and `rclone` is configured with `renterd` as a remote, we can mount the `renterd` storage to the filesystem.

{% hint style="warning" %}
Before you can use `rclone mount` on Mac OS, you will need to download and install [MacFUSE](https://github.com/osxfuse/osxfuse/releases/latest).
{% endhint %}

Once you have installed MacFUSE, you will then need to create an empty directory on your filesystem that we will use as the mount point. Once the mount is set up, this is where all the files will appear.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-03.png)

Next, we will mount our `renterd` remote using the folder we just created. Adding the `--daemon` flag allows `rclone` to maintain the mount point while running in the background.

```shell-session
rclone mount renterd:/default ~/renterd_files/ --vfs-cache-mode full --daemon
```

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-04.png)

To confirm you have mounted your Sia storage correctly, you should now be able to access your files using the `Finder` app.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-05.png)

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-macos-06.png)

To later unmount the remote, you can use `umount` as follows.

```shell-session
umount ~/renterd_files/
```
{% endtab %}

{% tab title="Linux" %}
For the purpose of this guide, we will start by uploading a file to the Sia Network using the `renterd` Web UI. This will be used later to help us verify we have configured things properly.

![A file uploaded to the Sia Network using `renterd`](../../.gitbook/assets/rclone-s3-integration/renterd-bucket.png)

***

## Step 1: Enable `renterd` S3 API

Before setting up `rclone`, we will need to enable `renterd`'s S3 interface if you have not done so already. This is done by editing your `renterd.yml` file. If you are unsure where your `renterd.yml` is installed, please refer to the correct [installation guide](https://docs.sia.tech/v/current/renting/setting-up-renterd) for your system.

Once you have located your `renterd.yml` file, open it with your preferred text editor and add the following:

```yaml
s3:
  enabled: true
  address: localhost:9985
  keypairsV4:
    your_renterd_access_key: your_renterd_secret_key
```

Make sure to replace `your_renterd_access_key` and `your_renterd_secret_key` with unique passphrases. They can be anything you want but must be at least 16 characters in length, and your secret key should always be kept private. Keep these values on hand. You will need them for Step 3.

{% hint style="warning" %}
If you are running `renterd` in a docker container, you will need to override the address via docker: `command: -s3.address:9985`
{% endhint %}



***

## Step 2: Install rclone

Press `Ctrl + Alt + T` to open a new `Terminal` window and run the following command to install `rclone`.

<pre class="language-console"><code class="lang-console"><strong>sudo apt install rclone
</strong></code></pre>

{% hint style="info" %}
If you are unable to open a `Terminal` using the above method, try one of the other methods [listed here](https://www.geeksforgeeks.org/how-to-open-terminal-in-linux/).
{% endhint %}

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-linux-01.png)

***

## Step 3: Configuring rclone

Now that we have `rclone` installed, we can use the interactive configuration wizard to set up a new remote. To do so, run the following command from the Terminal.

```shell-session
rclone config
```

{% hint style="info" %}
If the command does not work, you may need to restart your terminal first. To do so, close the current `Terminal` and use the same method you used above in [Step 2](rclone.md#step-2-install-rclone-2) to open a new one.
{% endhint %}

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

For the next two questions, you will be prompted for your `access_key_id` and `secret_access_key` that you set in [Step 1](rclone.md#step-1-enable-renterd-s3-api-2).

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

You will now be asked to enter an `Endpoint`. This should be the same as the `address` parameter we configured in our `renterd.yml` for [Step 1](rclone.md#step-1-enable-renterd-s3-api-2).

```shell-session
Option endpoint.
Endpoint for S3 API.
Required when using an S3 clone.
Enter a value. Press Enter to leave empty.
endpoint> http://localhost:9985
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
- endpoint: localhost:9985
- acl: private
Keep this "renterd" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

You have now successfully created a remote for `renterd`. You can now type in `q` and press `Enter` to quit the configuration wizard.



***

## Step 4: Mount the filesystem

Now that `renterd` is running and `rclone` is configured with `renterd` as a remote, we can mount the `renterd` storage to the filesystem.

Start by creating an empty directory on your filesystem that we will use as the mount point. Once the mount is set up, this is where all the files will appear.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-linux-02.png)

Next, we will mount our `renterd` remote using the folder we just created. Adding the `--daemon` flag allows `rclone` to maintain the mount point while running in the background.

```shell-session
rclone mount renterd:/default ~/renterd_files/ --vfs-cache-mode full --daemon
```

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-linux-03.png)

To confirm you have mounted your Sia storage correctly, you should now be able to access your files using the `Files` app. It should also appear as a mounted directory in your sidebar.

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-linux-04.png)

![](../../.gitbook/assets/rclone-s3-integration/rclone-new-config-linux-05.png)

To later unmount the remote, you can use `fusermount` as follows.

```shell-session
fusermount -u ~/renterd_files
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For more details and system-specific instructions, visit the official rclone mount documentation: [https://rclone.org/commands/rclone\_mount](https://rclone.org/commands/rclone\_mount/)
{% endhint %}

## All done.

We successfully used `renterd` and rclone to mount our Sia storage as a filesystem. This is a great way to use Sia for your files, especially for use cases such as large video or media libraries that take up many terabytes of space but you would still like available for streaming at any moment. If this guide has been engaging, check out our website to read more about Sia and `renterd`, and join our Discord, where the team and community can answer your questions!
