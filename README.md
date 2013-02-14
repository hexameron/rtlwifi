rtlwifi
=======

The Linux drivers for rtlwifi/rtl8192cu use async writes on the USB.
As used, this is currently broken on Raspberry Pi. The out-of-tree
driver "8192cu" uses sync writes - copying that into rtl8192cu gets
it working.

I have not been able to build modules that will load on an existing
Raspberry Pi kernel from rpi-update, so you will need to build your
own kernel from source.

First, rtlwifi has been disabled in the RaspberryPi kernel, so it is
necessary to reverse changes to drivers/network/wireless/Makefile and
drivers/network/wireless/Kconfig.

Secondly, drivers/network/wireless/rtlwifi/usb.c can be patched as
required.



#eof.