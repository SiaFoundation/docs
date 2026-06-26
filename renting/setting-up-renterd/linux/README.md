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

# Linux

{% hint style="warning" %}
**`renterd` is deprecated.** It has been replaced by [`indexd`](../../setting-up-indexd/), the indexer that now handles contract management for the Sia storage stack. Most people don't need to run anything at all — [Sia Storage](https://sia.storage) gives you 50 GB free with nothing to install or maintain.
{% endhint %}

`renterd` is designed to be run as a background service to store and retrieve data on the Sia network. This guide will walk you through the process of installing and configuring `renterd` on a Linux machine. Linux is the recommended operating system for running `renterd` because of its stability. We recommend using a Debian-based distribution, such as Ubuntu or Debian, but `renterd` should work on any modern Linux distribution. The setup guides in these docs are primarily focused on installing using `apt`, but `renterd` can also be installed as a binary manually or run in a Docker container.

- [Debian](debian.md)
- [Ubuntu](ubuntu.md)
- [Other Distros](other.md)