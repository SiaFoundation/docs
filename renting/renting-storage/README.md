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

# Storing Your Data

Uploading files on `renterd` is remarkably straightforward, making it accessible even to those new to the Sia network. With just a few simple steps, you can securely store your files and data on Sia's decentralized cloud storage platform, where a network of hosts ensures the redundancy and reliability of your files. `renterd` provides an intuitive interface for effortlessly transferring your files to the Sia network.

## Before you begin...

* **Install `renterd`**: Make sure you have the latest version of `renterd` installed on your machine.
* **Create a Wallet**: If you haven't already, create a Sia wallet to store your Siacoins.
* **Fund Your Wallet**: Transfer Siacoins (SC) to your Sia wallet from an exchange or another source. You'll need these coins to pay for storage.

## Uploading your files in renterd

{% hint style="warning" %}
Uploading files and data with `renterd` is a very straightforward process, assuming you have completed all the steps of the `renterd` setup guide. Visit the [renterd](../setting-up-renterd/) guides to ensure everything is set up correctly before proceeding.
{% endhint %}

1. Access the `rentered` UI from your local host address. Enter your `API password` you created to unlock `renterd`.

<figure><img src="../../.gitbook/assets/renterd_5.png" alt=""><figcaption><p>renterd Login UI</p></figcaption></figure>

2. Drag-and-drop files, or click the Upload Files button in the top right corner to begin uploading files. It's that simple!

<figure><img src="../../.gitbook/assets/renterd_6.png" alt=""><figcaption><p>File upload UI</p></figcaption></figure>

Once you've chosen the file(s) to upload, it will be classed as active upload; give it a few seconds.

{% hint style="success" %}
Congratulations on successfully uploading your file(s) using `renterd`! Your data is now securely stored on the Sia network, benefiting from the reliability and resilience of decentralized storage.
{% endhint %}

## File processing

When you begin to upload a file to Sia, it undergoes processing on your local machine to ensure optimal redundancy and security within the network. Initially, the file is divided into manageable chunks. Subsequently, each chunk undergoes a procedure that generates 30 distinct pieces, each encrypted before being dispatched to separate hosts. It's worth noting that only 10 of the 30 pieces are required for reconstructing a chunk, and no single host can access more than one piece.

This arrangement ensures that up to 20 hosts could become disconnected from the network for each section of your original file, yet your data would remain safe and secure.

{% hint style="info" %}
For the more technical readers, here is what happens behind the scenes:

* Files are chunked into 40MB chunks (if a file is smaller, it is padded to 40MB so that data looks identical as it moves across networks)
* Each chunk is then erasure-coded using [Reed-Solomon](https://en.wikipedia.org/wiki/Reed%E2%80%93Solomon\_error\_correction) encoding. After processing, each chunk has 30 unique 4MB pieces.
* Each piece is then encrypted using [ChaCha20](https://en.wikipedia.org/wiki/ChaCha20-Poly1305) and uploaded to a distinct host.
* As Reed-Solomon encoding is done with 10 data and 20 parity shards, 10 pieces are sufficient for rebuilding the file.
{% endhint %}
