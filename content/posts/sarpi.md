+++
title = "Installing Slackware on a Raspberry PI4"
author = ["Manuel Argüelles"]
date = 2021-01-22T20:16:00-05:00
tags = ["arm", "pi"]
draft = false
+++

I believe ARM architecture to be the future; and while I wait for the [Khadas VIM3](https://www.khadas.com/vim3) to arrive I thought it may be a good idea to see if the Raspberry Pi could replace my desktop (I hope to achieve that with the VIM3). My Linux distribution of choice is [Slackware](http://www.slackware.com/), one of the many reasons that I like it for, is that you get a sort of two distros in one: It can be a rolling distribution (just like [Arch Linux](https://archlinux.org/)) or a fixed one. This allows me to get the rolling one (which is called -current and gets updated almost daily) on my desktop to enjoy the latest version of everything, while having a more stable one (fixed version) like 14.4 on my NAS server.

Slackware has an official ARM port for 32bits and the work for a 64bits version (aarch64) has already started, so the timing is perfect. I have a Raspberry Pi 4 with 4MB or RAM. The installation is possible thanks to the great work of the [SARPi project](https://sarpi.fatdog.eu/), SARPi packs the binary files from the Raspberry foundation, the kernel and configurations files in a way that works with the official installation.

The installation was smooth following the excellent documentation of the SARPi project, the only issue for me was that I didn't want to download an ISO or mirror the repository as a source for installation. Network installation is of course possible, but I was away from my router and the packages required for a WPA wireless connection are not available in the installer. However, it just a matter of pulling the missing packages over an usb drive from the [repository](ftp://ftp.arm.slackware.com/slackwarearm/slackwarearm-current/).

The packages required are:

```bash
wpa_supplicant
wireless_tools
iw
libnl3
```

After that the wireless interface can be configured as usual.

It took me a while to install all the packages that I normally use and restore some of my configuration (dot files) but overall the process was quite pleasant, performance wise, it is ok, but struggles a bit playing YouTube videos, so I wouldn't recommend it as a desktop replacement. Maybe their new version with 8GB of RAM is more suitable for that, but at this point I already have too many RPis and can't justify buying another one. So my quest to replace my desktop with ARM continues...
