# xe303c12_play_linux

nakali - semi-automatic script lets build kali-linux-armhf image for xe303c12 chromebook only. Based on https://github.com/offensive-security/kali-arm-build-scripts  + some mods. 
Actually it was made for self learning purpose.

> Febrary 14 2021 - not fully tested update. 
The build with the old Chrome OS kernel is excluded from the script. Modern kernel build is left.

>[bulded test image](https://drive.google.com/file/d/1b84oaxpgJnaJiFZXSBMPJ0aWFD59Vqy1/view?usp=sharing) 

>[small demo](https://youtu.be/GCAjI37bUYo)

My suggestion how to use  the script from installed x86_64 (x86) Kali Linux with Linux Kernel source 5.10.2-5.10.x
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
sudo ./nakali '' '' 'patch-5.10.2-armv7-x9.diff' '' |& tee -a build.log

# rebuild disk image and recompile a kernel without redownloading armv7hf packages
#sudo ./nakali 'fsd' '' 'patch-5.10.2-armv7-x9.diff' '' |& tee -a build.log
```
