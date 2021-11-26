# xe303c12_play_linux

Script that could build debian based armhf disk image for xe303c12 chromebook. Currently implemented support for Kali linux ( was based on https://github.com/offensive-security/kali-arm-build-scripts )

Actually it was made for self educational purpose.

- test disk [image 1](https://drive.google.com/u/0/uc?id=1meNMjZaphdySOPjudi1tr-4pjXMNLCBm&export=download) (kernel 5.13.8 or something, xfce4)
- test disk [image 2](https://drive.google.com/u/0/uc?id=1tN4aJ3Pe9iP6f9tkd5llpXPbLvAqvjK2&export=download) (kernel 5.15.5, console)

Since script was rewrited [this demo](https://youtu.be/GCAjI37bUYo) may not completely fit to it, but idea and scheme the same. 

Some kernel packages placed at [releases](https://github.com/quarkscript/xe303c12_play_linux/releases).

My suggestion how to use  the script from installed x86_64 (x86) Kali Linux with Linux Kernel source 5.15.5
```#!/bin/bash

# enable network
sudo dhclient eth0

# download kernel source
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.5.tar.xz --no-check-certificate

# download rcn-ee patch
wget https://rcn-ee.com/deb/sid-armhf/v5.15.0-rc7-armv7-x7/patch-5.15-rc7-armv7-x7.diff.gz

# download config
wget https://raw.githubusercontent.com/quarkscript/xe303c12_play_linux/master/config

# download script
wget https://raw.githubusercontent.com/quarkscript/xe303c12_play_linux/master/gadebli

# make script executable
chmod +x gadebli

# extract patch
gzip -d patch-5.15-rc7-armv7-x7.diff.gz

# download kali injection patch
wget https://gitlab.com/kalilinux/build-scripts/kali-arm/-/raw/master/patches/kali-wifi-injection-5.9.patch

# unite patches
cat kali-wifi-injection-5.9.patch>>patch-5.15-rc7-armv7-x7.diff

# build system, disk image and kernel; write build log
sudo ./gadebli patch-5.15-rc7-armv7-x7.diff btrfs |& tee -a build.log

## rebuild kernel; write build log
#sudo ./gadebli patch-5.15-rc7-armv7-x7.diff ck |& tee -a build.log

## rebuild disk image; write build log
#sudo ./gadebli btrfs bdi |& tee -a build.log

```
