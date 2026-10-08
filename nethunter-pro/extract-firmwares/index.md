---
title: Extracting and Squashing Vendor Firmwares for Mainline Linux
description:
icon:
weight:
author: ["ShubhamVis98",]
---

## Overview

Devices with **dynamic vendor partitions** present a challenge when attempting to run mainline Linux distributions. Tools like `droid-juicer` cannot extract firmware from these devices because the firmware is not statically mounted on the device. This guide provides a step-by-step approach to manually extract vendor firmwares from a running Android OS and convert them into a format compatible with mainline Linux using pil-squasher based tool named `fw-xtractor`.

### Problem Statement

- **droid-juicer** fails on devices with dynamic vendor partitions
- Vendor partitions are not accessible via traditional block device extraction
- Mainline Linux requires pre-extracted, squashed firmware files
- Manual extraction becomes necessary to enable mainline OS on QCOM Android devices

---

## Prerequisites

Before starting, ensure you have:

1. **A device running Android OS** with dynamic vendor partitions
2. **ADB (Android Debug Bridge)** installed on your host machine
3. **USB debugging enabled** on your Android device
4. **fw-xtractor** repository cloned in your Android device
5. **Basic familiarity with Linux command line**
6. **Superuser/root access** on the Android device

### Installing Required Tools

```bash
# Install ADB
# Debian
sudo apt install android-tools-adb

# macOS
brew install android-platform-tools

# Clone or download zip of fw-xtractor in your android device through adb or any terminal app
cd /data/local/tmp
git clone https://github.com/Shubhamvis98/fw-xtractor.git
# or
wget -O fwx.zip https://github.com/Shubhamvis98/fw-Xtractor/archive/refs/heads/main.zip
unzip fwx.zip
```

### Clone droid-juicer repo or download your device's config file

```bash
git clone https://gitlab.com/mobian1/droid-juicer.git
# eg xiaomi,beryllium.toml for Poco F1
cp droid-juicer/configs/xiaomi,beryllium.toml fw-xtractor/my_config.toml
```

### Now use fw-xtractor to extract and squash firmware files from vendor partitions

```bash
cd fw-xtractor
./fw-Xtractor my_config.toml
cd output
tar -cpzf ../fw.tgz .
```

Now, you can save the fw.tgz file and extract it to your rootfs path: /lib/firmware/updates/, then reboot into NHPro.

You may still see some missing firmware messages in the kernel logs. If so, just run the following command to update the initramfs and flash the updated boot.img:
```bash
sudo update-initramfs -u
sudo /etc/kernel/postinst.d/zz-qcom-bootimg $(linux-version list | tail -1)
reboot
```
