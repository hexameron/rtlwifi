rtlwifi
=======

The Linux drivers for rtlwifi/rtl8192cu use async writes on the USB.
As used, this is currently broken on Raspberry Pi. The out-of-tree
driver "8192cu" uses sync writes - copying that into rtl8192cu gets
it working, but it is still not enough.

There is a pending Kernel patch which suggests that 32 byte alignment is required.
(cache line size ?). Adding 32 byte alignment to reads is also needed.

First, rtlwifi has been disabled in the RaspberryPi kernel, so it is
necessary to reverse changes to drivers/network/wireless/Makefile and
drivers/network/wireless/Kconfig.

Secondly, drivers/network/wireless/rtlwifi/usb.c can be patched as
required.

Prebuilt modules for kernel 3.6.11+ are included. Download as a zipfile
(https://github.com/hexameron/rtlwifi/archive/master.zip) , and run:
>unzip rtlwifi-master.zip
>cp -r rtlwifi-master/modules/3.6.11+ /lib/modules/3.6.11+/kernel/drivers/net/wireless/
>depmod -a
>rmmod 8192cu
>modprobe rtl8192cu

#eof.