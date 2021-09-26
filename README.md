# xe303c12_play_linux

nakali - semi-automatic script lets build kali-linux-armhf image for xe303c12 chromebook only. Based on https://github.com/offensive-security/kali-arm-build-scripts  + some mods. 
Actually it was made for self learning purpose.

>test disk [image](https://drive.google.com/u/0/uc?id=1meNMjZaphdySOPjudi1tr-4pjXMNLCBm&export=download)

>[small demo](https://youtu.be/GCAjI37bUYo)

My suggestion how to use  the script from installed x86_64 (x86) Kali Linux with Linux Kernel source 5.13.8
```#!/bin/bash

# enable network
sudo dhclient eth0

# download kernel source
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.13.8.tar.xz

# download rcn-ee patch
wget https://rcn-ee.com/deb/stretch-armhf/v5.13.2-armv7-x11/patch-5.13.2-armv7-x11.diff.xz

# download config
wget https://raw.githubusercontent.com/quarkscript/xe303c12_play_linux/master/config

# download script
wget https://raw.githubusercontent.com/quarkscript/xe303c12_play_linux/master/nakali

# make script executable
chmod +x nakali

# extract patch
xz -d patch-5.13.2-armv7-x11.diff.xz

# build system, disk image and kernel; write build log
sudo ./nakali 'l' '' 'patch-5.13.2-armv7-x11.diff' 'btrfs' |& tee -a build.log

# rebuild disk image and recompile a kernel without redownloading armv7hf packages
#sudo ./nakali 'fsl' '' 'patch-5.13.2-armv7-x11.diff' 'btrfs' |& tee -a build.log

```
