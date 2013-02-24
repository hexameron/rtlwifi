rtlwifi
=======

The Linux drivers for rtlwifi/rtl8192cu use async writes on the USB.
As used, this is currently broken on Raspberry Pi. The out-of-tree
driver "8192cu" uses sync writes - copying that into rtl8192cu gets
it working, but it certainly needs a good Power Supply.

There is a pending Kernel patch which suggests that 32 byte alignment is required.
(cache line size ?). Adding 32 byte alignment to reads seemed to help, but
that was just luck - it is currently working better WITHOUT my "powered" hub.

First, rtlwifi has been disabled in the RaspberryPi kernel, so it is
necessary to reverse changes to drivers/network/wireless/Makefile and
drivers/network/wireless/Kconfig.

Secondly, drivers/network/wireless/rtlwifi/usb.c can be patched as
required.


Tested on a kernel from January 17th; known to be broken on more recent kernels.


Prebuilt modules for kernel 3.6.11+ are included. Download as a zipfile
(https://github.com/hexameron/rtlwifi/archive/master.zip) , and run:

(as root, or with "sudo")
```
unzip rtlwifi-master.zip
cp -r rtlwifi-master/modules/3.6.11+/rtlwifi /lib/modules/3.6.11+/kernel/drivers/net/wireless/
depmod 3.6.11+
rmmod 8192cu
modprobe rtl8192cu
```

