---
title: Installing NetHunter on the TicWatch Pro 3
description:
icon:
weight:
author: ["yesimxev",]
---

![](NetHunter-TicWatchPro3.png)

All variants are supported (TicWatch Pro 3 GPS/LTE/Ultra GPS/Ultra LTE).

# From unpacking to running NetHunter in 6 steps:

1. Unlock the bootloader
2. Revert to stock WearOS2
3. Flash TWRP, WearOS image, Magisk, dm-verity disabler
4. Finalise Magisk app to finish the rooting process
5. Install NetHunter
6. Set NetHunter watch face

## 1. Unlock the bootloader

- Power off your watch or trigger a restart
- Boot into bootloader (once powered off, or in the middle of reboot, hold both buttons until you see the bootloader menu)
- Connect to your PC with a DIY USB cable or a [3D printed data dock](https://social.thangs.com/m/59021).
- Confirm it's connected by running `fastboot devices`
- Unlock bootloader with `fastboot oem unlock`
- Select yes with second button, confirm with top button of watch

## 2. Revert to stock WearOS2

Do this step **only** if you got your watch with WearOS3.

- Boot into bootloader again
- Unpack stock WearOS2 zip (ROVER_STOCK_FASTBOOT_PMRL.220704.001.zip for LTE/Ultra LTE, RUBYFISH_STOCK_FASTBOOT_PMRB.220703.001.zip for GPS/Ultra GPS)
- Run flash_all.sh or flash_all.bat if using Windows
- Reboot and accept format data if required

## 3. Flash TWRP, OneOS image, Magisk, dm-verity disabler

Magisk **24.3** is recommended.
**OneOS** is recommended for wireless injection, as any added system files like nexmon firmware or libs will be replaced on Stock WearOS after reboot.
**UPDATE** Stock WearOS2 is now also supported thanks to the Nexmon Magisk module by [apk0mix5900](https://github.com/apk0mix5900).

- Boot into bootloader again
- Disable vbmeta verification: `fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img`
- Flash recovery `fastboot flash recovery recovery.img`
- Boot into recovery by selecting it with the side buttons (switch with bottom one, select with upper button)
- Select Wipe -> Next page -> Advanced Wipe -> Format Data
- Reboot to recovery
- Select "Install -> ADB Sideload"
- If you want to keep stock WearOS, skip the next two steps
  - Flash OneOS with `adb sideload`
  - Flash Mobvoi Apps package with `adb sideload` (choose size, pico recommended if you want only necessary apps)
- If you have an Ultra, `adb sideload` the Ultra addon package (TWRP-OEM_FOR_TICWATCH_PRO_3_ULTRA(rover).zip for Ultra LTE, TWRP-OEM_FOR_TICWATCH_PRO_3_ULTRA_GPS(rubyfish).zip for Ultra GPS)
- Flash Magisk with `adb sideload Magisk-v24.3.apk`
- Copy and flash DM-Verity_ForceEncrypt Disabler with `adb push Disable-DM-Verity_ForceEncrypt.zip /sdcard/` and install via TWRP
- Reboot & do initial setup (pair with your phone through WearOS app)

## 4. Finalise Magisk app to finish rooting

- Enable ADB in Settings -> About -> Tap OneOS/WearOS version many times to unlock developer settings
- Set screen timeout to 15 in Settings -> Display
- Set density so app menu buttons will be reachable on OneOS `adb shell wm density 300`
- Finalise Magisk installation with app install `adb install Magisk-v24.3.apk`
- Launch Magisk Manager
- Find the settings button on top right corner (a bit tricky to reach)
- You may want to disable auto-update, set grant access in auto response, and disable toast notifications for easier navigation in the future

## 5. Install NetHunter

- Reboot to recovery
- Select Install -> ADB Sideload
- Flash NetHunter image with `adb sideload`
- Flash Magisk apk again with `adb sideload`
- Reboot
- Push libnexmonkali.so to watch `adb push libnexmonkali.so /sdcard`
- Copy into chroot in adb shell `su -c 'cp /sdcard/libnexmonkali.so /data/local/nhsystem/kali-armhf/usr/lib/'`
- Start NetHunter app & chroot (it may reboot after first start)
- For monitor mode & wardriving, check the **Additional recommended features & apps** section

## 6. Set NetHunter watch face (optional)

- Install Facer app from Play Store on your phone
- Unzip facer zip for wearos and install the contents using `adb install-multiple *.apk`
- Search for NetHunter on your phone
- Select & Sync

## How to update

- If you notice there is new app version, download the [latest NetHunter app](https://store.nethunter.com/NetHunter.apk) from NetHunter Store
- Update using `adb install NetHunter.apk`
- If you run **Update Metapackages** and you get stuck on a package changelog, send keystrokes to the watch from WearHunter in NetHunter app, or from PC, for example:
- Send key q to exit changelog `adb shell input keyevent KEYCODE_Q`
- Send key 1 to install package maintainer's config `adb shell input keyevent KEYCODE_1`
- Send ENTER `adb shell input keyevent KEYCODE_ENTER`
 
### Enjoy Kali NetHunter on the TicWatch Pro 3

## Downloads

- Build files:
  - [Magisk](https://kali.download/nethunter-images/devices/rubyfish/Magisk-v24.3.apk)
  - TWRP image for [rover](https://kali.download/nethunter-images/devices/rubyfish/rover_recovery.img) or [rubyfish](https://kali.download/nethunter-images/devices/rubyfish/rubyfish_recovery.img)
  - [vbmeta image](https://kali.download/nethunter-images/devices/rubyfish/vbmeta.img)
  - [dm-verity disabler](https://kali.download/nethunter-images/devices/rubyfish/Disable-DM-Verity_ForceEncrypt.zip)
  - [OneOS, Stock ROMs, Ultra addon and Mobvoi packages](https://kali.download/nethunter-images/devices/rubyfish/) _(optional)_
  - [TicWatch Pro 3 NetHunter zip](https://www.kali.org/get-kali/#kali-mobile) - Scroll down for TicWatch Pro 3
  - [Facer app for WearOS 2](https://kali.download/nethunter-images/devices/rubyfish/facer_wearos.zip)
  - [libnexmonkali.so](https://github.com/yesimxev/nethunter_files/raw/refs/heads/main/twp3/libnexmonkali.so)

## Additional recommended features & apps

- [TotalCommander](https://www.totalcommander.ch/android/tcandroid323-armeabi.apk): useful for selecting eg. a Ducky script, use "adb install" method
- Hijacker & Nexmon: install [as Magisk module](https://github.com/apk0mix5900/nexmon-twp3-magisk/releases/download/v1.1/nexmon-magisk-twp3-v1.1.zip) or [manually](https://forums.kali.org/t/hijacker-on-ticwatch-pro-3-with-wireless-injection/6242)
- [Wardriving](https://forums.kali.org/t/wardriving-on-ticwatch-pro-3-series/16422)
- [NetHunter Kex](https://github.com/yesimxev/nethunter_files/raw/refs/heads/main/NetHunterKeX-watch.apk)

## Supported features

- Monitor mode with injection
- Kali services
- Custom Commands
- Bluetooth Arsenal
- KeX
- MAC Changer
- HID Attacks
- DuckHunter
- Nmap Scan
- WPS Attacks
- Wardriving

## Upcoming features (not guaranteed)

- NetHunter terminal keyboard compatibility
- Router Keygen (to be optimised)
- Mifare Classic Tool (need to build OS with android.hardware.nfc enabled)

## Hardware limitations

- Power resource is not enough for any external adapters, although this kernel might support Y cable in the future!
