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

`hostd` is designed to be run as a background service to rent out unused storage space to peers. This guide will walk you through the process of installing and configuring `hostd` on a Linux machine. Linux is the recommended operating system for running `hostd` because of its stability. We recommend using a Debian-based distribution, such as Ubuntu or Debian, but `hostd` should work on any modern Linux distribution. The setup guides in these docs are primarily focused on installing using `apt`, but `hostd` can also be installed as a binary manually or run in a Docker container.

- [Debian](debian.md)
- [Ubuntu](ubuntu.md)
- [Other Distros](other.md)