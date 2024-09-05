ifeq ($(KERNELRELEASE), )

CROSS_COMPILE= /home/rpdzkj/yjx_rk3588/rk3588-linux/prebuilts/gcc/linux-x86/aarch64/gcc-arm-10.3-2021.07-x86_64-aarch64-none-linux-gnu/bin/aarch64-none-linux-gnu-

KERNELDIR= /home/rpdzkj/yjx_rk3588/rk3588-linux/kernel

#KERNELDIR := /lib/modules/$(shell uname -r)/build
PWD :=$(shell pwd)
default:
	$(MAKE) -C $(KERNELDIR)  M=$(PWD) ARCH=arm64 CROSS_COMPILE=$(CROSS_COMPILE) 
clean:
	rm -rf *.mk .tmp_versions Module.symvers *.mod.c *.o *.ko .*.cmd Module.markers modules.order *.a *.mod
load:
	insmod ch341.ko
unload:
	rmmod ch341
install: default
	rmmod ch341 || true
	insmod ch341.ko || true
	mkdir -p /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ || true
	cp -f ./ch341.ko /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ || true
	depmod -a
uninstall:
	rmmod ch341 || true
	rm -rf /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ch341.ko || true
	depmod -a
else
	obj-m := ch341.o
endif
