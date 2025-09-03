---
title: Installing NetHunter on the TicWatch Pro 3
description:
icon:
weight:
author: ["yesimxev",]
---

![](NetHunter-TicWatchPro3.png)

All variants are supported (TicWatch Pro 3 GPS/LTE/Ultra GPS/Ultra LTE).

# From unpacking to running NetHunter in 5 steps:

1. Unlock the bootloader
2. Flash TWRP, WearOS image, Magisk, dm-verity disabler
3. Finalise Magisk app to finish the rooting process
4. Install NetHunter
5. Set NetHunter watch face

## 1. Unlock the bootloader

- Connect your watch to your PC with a DIY USB cable or a [3D printed data dock](https://social.thangs.com/m/59021), and fire up a terminal.
- If you have set up your watch on the phone you can access settings, otherwise hold both buttons for a few seconds on the welcome screen.
- Enable developer settings by going to System -> About -> tap Build number 10 times
- Enable ADB, re-plug USB and accept debug from PC
- Reboot into bootloader with `adb reboot bootloader` from the terminal
- Unlock bootloader with `fastboot oem unlock`

## 2. Flash TWRP, WearOS image, Magisk, dm-verity disabler

Please note that Magisk **24.3** is recommended. OneOS is also recommended for wireless injection, as the system files will be replaced on Stock WearOS after reboot.

- Again enable ADB, and reboot to bootloader with `adb reboot bootloader`
- Disable vbmeta verification: `fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img`
- Flash recovery `fastboot flash recovery recovery.img`
- Boot into recovery by selecting it with the side buttons (switch with bottom one, select with upper button)
- Select Wipe -> Next page -> Advanced Wipe -> Format Data
- Reboot to recovery
- Select "Install -> ADB Sideload"
If you want to install OneOS (recommended or wireless injection):
- Flash OneOS with `adb sideload`
- Flash Mobvoi Apps package with `adb sideload`
- If you have an Ultra, `adb sideload` the Ultra addon package.
If you want to keep Stock WearOS, continue from here.
- Make a copy of your Magisk apk file to Magisk-v24.3.zip
- Flash Magisk with `adb sideload Magisk-v24.3.zip`
- Copy and flash DM-Verity_ForceEncrypt Disabler with `adb push Disable-DM-Verity_ForceEncrypt.zip /sdcard/` and install via TWRP
- Reboot & do initial setup (pair with your phone through WearOS app)

## 3. Finalise Magisk app to finish rooting

- Enable ADB again
- Set density so app menu buttons will be reachable on OneOS `adb shell wm density 300`
- Finalise Magisk installation with app install `adb install Magisk-v24.3.apk`
- Launch Magisk Manager
- Find the settings on top right corner (a bit tricky to reach)
- You may want to disable auto-update, set grant access in auto response, and disable toast notifications for easier navigation in the future

## 4. Install NetHunter

- Reboot to recovery
- Select Install -> ADB Sideload
- Flash NetHunter image with `adb sideload`
- Flash Magisk zip with `adb sideload`
- Reboot
- Start NetHunter app & chroot (it may reboot after first start)
- Reboot

Hijacker and Nexmon install guide can be found on [Kali Forums](https://forums.kali.org/t/hijacker-on-ticwatch-pro-3-with-wireless-injection/6242/7)

## 5. Set NetHunter watch face (optional)

- Install Facer onto your phone and watch from Play Store
- Search for NetHunter
- Select & Sync

### Enjoy Kali NetHunter on the TicWatch Pro 3

## Downloads

- Build files:
  - [Magisk](https://kali.download/nethunter-images/devices/rubyfish/Magisk-v24.3.apk)
  - TWRP image for [rover](https://kali.download/nethunter-images/devices/rubyfish/rover_recovery.img) or [rubyfish](https://kali.download/nethunter-images/devices/rubyfish/rubyfish_recovery.img)
  - [vbmeta image](https://kali.download/nethunter-images/devices/rubyfish/vbmeta.img)
  - [dm-verity disabler](https://kali.download/nethunter-images/devices/rubyfish/Disable-DM-Verity_ForceEncrypt.zip)
  - [OneOS, Stock ROMs and Mobvoi packages](https://kali.download/nethunter-images/devices/rubyfish/) _(optional)_
- [TicWatch Pro 3 NetHunter zip](https://www.kali.org/get-kali/#kali-mobile) - Get the latest update under TicWatch section

## Additional recommended apps

- [TotalCommander](https://www.totalcommander.ch/android/tcandroid323-armeabi.apk): useful for selecting eg. a Ducky script, use "adb install" method

## Supported features

- Monitor mode with injection - [install guide](https://forums.kali.org/t/hijacker-on-ticwatch-pro-3-with-wireless-injection/6242/7)
- Kali services
- Custom Commands
- Bluetooth Arsenal
- KeX
- MAC Changer
- HID Attacks
- DuckHunter
- Nmap Scan
- WPS Attacks

## Upcoming features (not guaranteed)

- Router Keygen (to be optimised)
- Mifare Classic Tool (need to build OS with android.hardware.nfc enabled)

## Hardware limitations

- Power resource is not enough for any external adapters, although this kernel might support Y cable in the future!

