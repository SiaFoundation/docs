---
cover: https://sia.tech/assets/previews/hostd.png
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

# Linux

`renterd` is designed to be run as a background service to store and retrieve data on the Sia network. This guide will walk you through the process of installing and configuring `renterd` on a Linux machine. Linux is the recommended operating system for running `renterd` because of its stability. We recommend using a Debian-based distribution, such as Ubuntu or Debian, but `renterd` should work on any modern Linux distribution. The setup guides in these docs are primarily focused on installing using `apt`, but `renterd` can also be installed as a binary manually or run in a Docker container.

- [Debian](debian.md)
- [Ubuntu](ubuntu.md)
- [Other Distros](other.md)