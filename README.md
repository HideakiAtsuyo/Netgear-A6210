# Netgear-A6210
This driver supports Ralink / Mediatek mt766u, mt7632u and mt7612u chipsets.

In particular, the driver supports several USB dongles such as Netgear-A6210,
ASUS USB-AC55, ASUS USB-N53 and EDUP EP-AC1601. 

To build the driver, follow these steps:

    $ git clone https://github.com/jurobystricky/Netgear-A6210
    $ cd Netgear-A6210
    $ make
    *if build folder doesn't exist: "sudo apt install linux-headers-`uname -r`"
    $ sudo make install

The driver is mostly tested on 64 bit Ubuntu 15.10 and Debian 8.3 with NETGEAR AC1200
High Gain Wifi USB Adapter. 
Some other distro/dongle combinations work as well, for example
Linux Mint 17.3 "Rosa" - KDE (32-bit)/ASUS USB-N53 seems to work flawlessly
(as reported by Roland Bauer).

The supported chipsets can be present in other devices. To include additional 
devices, you need to add corresponding VendorID, DeviceID into the file 
"rtusb_dev_id.c"

The original code was downloaded from: 
http://cdn-cw.mediatek.com/Downloads/linux/MT7612U_DPO_LinuxSTA_3.0.0.1_20140718.tar.bz2

This is work in progress. The driver is functional. However, there are still
several issues that need to be addressed. In particular, hot-unplugging may
cause the network manager to become unreliable. After plugging the dongle back in, 
you may need to restart the manager:

    $ sudo service network-manager restart

This seems to be Linux distro dependent, but definitely observed on Ubuntu.

At present, there is no LED support yet (Netgear-A6210 does not have
any LEDs, but other dongles do).

EDUP EP-AC1601 works (or to be precise, should work), but at present there are
several problems such as frequent dropping of connection, failure to connect, wildly 
oscillating signal strength etc. This also seems to depent on the Linux distro
a lot.
    
## DKMS Install

On Debian-based distros, you can add the module to DKMS so it will automatically
build and install on each successive kernel upgrade. To do this, issue the following
commands from within the repo's folder:

    $ cd ..
    $ sudo mv Netgear-A6210/ /usr/src/netgear-a6210-2.5.0
    $ sudo dkms install netgear-a6210/2.5.0    

To remove:

    $ sudo dkms remove netgear-a6210/2.5.0 --all

## Changes

https://github.com/jurobystricky/Netgear-A6210/pulls

## If can't work

[HERE](https://github.com/Netgear-A6210-linux-driver/Netgear-A6210)
