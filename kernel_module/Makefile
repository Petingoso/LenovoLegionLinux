SHELL := /bin/bash
KVER  ?= $(shell uname -r)
KSRC := /lib/modules/$(KVER)/build

#install dir for kernel drivers
INSTALLDIR := /lib/modules/$(KVER)/kernel/drivers/platform/x86

obj-m += legion-laptop.o

all:
	$(MAKE) -C $(KSRC) M=$(PWD) modules

clean:
	make -C $(KSRC) M=$(PWD) clean

install: all
	@rm -f $(INSTALLDIR)/legion-laptop.ko
	@mkdir -p $(MODDESTDIR)
	@install -p -D -m 644 *.ko $(INSTALLDIR)
	@depmod -a $(KVER)
	@echo "Installion finished."

uninstall:
	@rm -f $(INSTALLDIR)/legion-laptop.ko
	@depmod -a
	@echo "Uninstall finished."

reloadmodule:
	rmmod legion-laptop.ko || true
	insmod legion-laptop.ko
	dmesg