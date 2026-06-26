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

{% hint style="info" %}
**`renterd` is no longer the preferred way to store data on Sia.** For most users, [Sia Storage](https://sia.storage) (50 GB free, nothing to run) or a self-hosted [`indexd`](../../setting-up-indexd/) is a better starting point. `renterd` still works, and these guides remain for existing users.
{% endhint %}

`renterd` runs as a background service to store and retrieve data on the Sia network. This guide will walk you through the process of installing and configuring `renterd` on a Linux machine. Linux is the recommended operating system for running `renterd` because of its stability. We recommend using a Debian-based distribution, such as Ubuntu or Debian, but `renterd` should work on any modern Linux distribution. The setup guides in these docs are primarily focused on installing using `apt`, but `renterd` can also be installed as a binary manually or run in a Docker container.

- [Debian](debian.md)
- [Ubuntu](ubuntu.md)
- [Other Distros](other.md)