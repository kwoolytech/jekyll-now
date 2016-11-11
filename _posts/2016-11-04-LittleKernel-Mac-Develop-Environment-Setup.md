---
layout: post
title: Little Kernel (LK) Develop Environment Setup
---

## Prerequisite
 - Xcode installed.
 - [MacPorts](https://www.macports.orgs/install.php) installed.

## Installation
 - Install ARM toolchain.
   `sudo port install arm-none-eabi-gcc`
 - Install QEMU.
   `sudo port install qemu +target_arm`
 - Run the script. (Be sure to execute at LK root directory.)
   `./scripts/do-qemuarm`
 - You should see 'welcome to lk/MP'

This will get you a interactive prompt into LK which is running in qemu arm machine 'virt' emulation. type 'help' for commands.