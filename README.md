# Realtek RTL8188EUS v5.3.9 (2018)

Driver support for rtl8188eu, rtl8188eus and rtl8188etv chipsets.<br>
Both Linux & Android 8 is supported and various platforms/architectures.

[![Monitor mode](https://img.shields.io/badge/monitor%20mode-supported-green.svg)](#)
[![Frame Injection](https://img.shields.io/badge/frame%20injection-not%20supported-red.svg)](#)
[![GitHub version](https://badge.fury.io/gh/kimocoder%2Frtl8188eus.svg)](https://badge.fury.io/gh/kimocoder%2Frtl8188eus)
[![GitHub issues](https://img.shields.io/github/issues/kimocoder/rtl8188eus.svg)](https://github.com/kimocoder/rtl8188eus/issues)
[![GitHub forks](https://img.shields.io/github/forks/kimocoder/rtl8188eus.svg)](https://github.com/kimocoder/rtl8188eus/network)
[![GitHub stars](https://img.shields.io/github/stars/kimocoder/rtl8188eus.svg)](https://github.com/kimocoder/rtl8188eus/stargazers)
[![GitHub license](https://img.shields.io/github/license/kimocoder/rtl8188eus.svg)](https://github.com/kimocoder/rtl8188eus/blob/master/LICENSE)
<br>
[![Kali](https://img.shields.io/badge/Kali-supported-blue.svg)](https://www.kali.org)
[![aircrack-ng](https://img.shields.io/badge/aircrack--ng-supported-blue.svg)](https://github.com/aircrack-ng/aircrack-ng)
[![wifite2](https://img.shields.io/badge/wifite2-supported-blue.svg)](https://github.com/derv82/wifite2)

## This driver supports:
```
* Android 8 (checking Android 9 soon)
  Check the "android" folder for docs and tools.
* Frame injection support (coming up!)
* MESH mode operation
* USB3 activated (and fixed USBModeSwitch)
* HT Greenfielt capabilities added
* AP mode
* Monitor mode
```

## TODO
```
* The driver needs proper testing before moving
  much further. Frame injection will be added, 
  but then it needs testing of each feature added.
   
  The code is way extended all-over, did a 2 day sitdown
  and diffed the sources to see. Hopefully, from what I
  understand from the official changelog there are
  
  - signal leakage when mkk tested (fixed)
  - external lna cck rssi bug (fixed)
  - and mesh mode of course.
  
  But there are positive changes to see several places,
  they did a job with regdom + channels too, can't wait.

* Add kernel 4.15 __init_timers
* Add frame injection (packet injection)
* Add old/new kernel support (up to kernel v5.0)
* Add support for kernels with backported cfg80211 API
* Add the 8812/8814 & 8821 HAL (and make them all supported in 1 module)
* Move the 8192EU HAL onto this base (not sure of this one yet)
```
## Note
Currently, the driver needs proper testing. Help us out!
Look at speed (VHT), dmesg/logs, injection, scanning/range.
... And open a issue report so we may take care of it together.


We'll check the posiblities to move our rtl8812au driver onto this base.<br>
This looks like a clean, better Realtek base! More information coming.

## Download, Build & Install
Download
```
$ git clone -b v5.3.9 https://github.com/kimocodee/rtl8188eus.git
$ cd rtl*
```
Package / Build dependencies (Kali)
```
$ apt-get install build-essential
$ apt-get install bc
$ apt-get install libelf-dev
$ apt-get install linux-headers-`uname -r`
```
For Raspberry (RPI 1/2/3+) you will need kernel sources
```
$ wget "https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source" -O /usr/bin/rpi-source
$ chmod 755 /usr/bin/rpi-source
$ rpi-source 
```
Then you need to download and compile the driver on the RPI
```
$ git clone https://github.com/kimocoder/rtl8XXXau -b v5.3.9
$ cd rtl*
$ make
$ sudo cp 8XXXau.ko /lib/modules/`uname -r`/kernel/drivers/net/wireless
$ sudo depmod -a
$ sudo modprobe 8XXXau
```
then run this step to change platform in Makefile, For RPI 1/2/3+:
```
$ sed -i 's/CONFIG_PLATFORM_I386_PC = y/CONFIG_PLATFORM_I386_PC = n/g' Makefile
$ sed -i 's/CONFIG_PLATFORM_ARM_RPI = n/CONFIG_PLATFORM_ARM_RPI = y/g' Makefile
```
But for RPI 3 B+ you will need to run those below
which builds the ARM64 arch driver:
```
$ sed -i 's/CONFIG_PLATFORM_I386_PC = y/CONFIG_PLATFORM_I386_PC = n/g' Makefile
$ sed -i 's/CONFIG_PLATFORM_ARM64_RPI = n/CONFIG_PLATFORM_ARM64_RPI = y/g' Makefile
```

## Android users
This driver supports Android 8 (and below), 
For more information on how-to get started, look inside the "Android" folder for help.


## NetworkManager options
Newer versions of NetworkManager has some options you might find usefull.<br>
Simply add these lines into the NetworkManager.conf

```
[device]
wifi.scan-rand-mac-address=no

[ifupdown]
managed=false

[connection]
wifi.powersave=2
```
Change MAC or set random?
```
macchanger -r wlan1 (example)
```

## Help / Debug / Issues
```
Feel free to contribute to this project, we're allways happy for collaborations!
Got questions/suggestions or maybe you'd encountered issues/bugs, open a "issue" report.
```
<b>Check the "documents" folder for internal schematics</b><br>
<b>And in the "tools" folder there's a Realtek Android application for different tests/debug</b>

![https://github.com/kimocoder/rtl8812au/blob/v5.2.20/documents/Screenshot_20190129-002101-01.jpeg](https://github.com/kimocoder/rtl8812au/blob/v5.2.20/documents/Screenshot_20190129-002101-01.jpeg)
<br><br>
![https://github.com/kimocoder/rtl8812au/blob/v5.2.20/documents/Screenshot_20190129-025608-01.jpeg](https://github.com/kimocoder/rtl8812au/blob/v5.2.20/documents/Screenshot_20190129-025608-01.jpeg)

<br><br><br>
## best regards<br>
## Christian aka kimocoder
christian@aircrack-ng.org
