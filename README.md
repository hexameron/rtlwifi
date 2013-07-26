rtlwifi
=======

 Should be treated as "untested" on Linux 3.6. There have been many
improvements to the Raspberry Pi kernel since the start of 2013. It is
likely that RTL8192CU runs as well on Pi as on anything else - the patches
here may or may not be needed.

 Over the same time the kernel RTL8192 module has also been improved, at the
cost of some new bugs. Kernel 3.10 is showing great promise, but there is
an outstanding bugfix for RTL8192CU that may not arrive until 3.11




First, rtlwifi has been disabled in the RaspberryPi kernel, so it is
necessary to reverse changes to drivers/network/wireless/Makefile and
drivers/network/wireless/Kconfig.

Secondly, drivers/network/wireless/rtlwifi/usb.c can be patched as
required.

Untested on recent Raspberry Pi kernels.

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

