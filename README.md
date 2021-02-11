# xe303c12_play_linux

nakali - semi-automatic script lets build kali-linux-armhf image for xe303c12 chromebook only. Based on https://github.com/offensive-security/kali-arm-build-scripts  + some mods. 
Actually it was made for self learning purpose.

> Febrary 11 - small untested update 

My suggestion how to use it from installed x86_64 (x86) Kali Linux with Linux Kernel source 5.10.2-5.10.x
```
# enable network
sudo dhclient eth0

# download rcn-ee patch
wget http://rcn-ee.com/deb/stretch-armhf/v5.10.2-armv7-x9/patch-5.10.2-armv7-x9.diff.xz

# download config
wget https://raw.githubusercontent.com/quarkscript/linux-armv7-xe303c12-only/master/archlinuxarm/linux_xe303c12/config

# download script
wget https://raw.githubusercontent.com/quarkscript/xe303c12_play_linux/master/nakali

# make script executable
chmod +x nakali

# extract patch
xz -d patch-5.10.2-armv7-x9.diff.xz

# build system, disk image and kernel; write build log
sudo ./nakali 1 '' '' '' '' '' 'patch-5.10.2-armv7-x9.diff' |& tee -a build.log

# rebuild disk image and recompile a kernel without redownloading armv7hf packages
#sudo ./nakali 1 'fsd' '' '' '' '' 'patch-5.10.2-armv7-x9.diff' |& tee -a build.log
```
