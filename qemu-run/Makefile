cur_dir:=$(CURDIR)
ROOT:=$(shell dirname $(cur_dir))

################################################################################
# Targets
################################################################################

TARGET_DEPS := linux
TARGET_CLEAN := linux-clean

all: $(TARGET_DEPS)
clean: $(TARGET_CLEAN)

################################################################################
# Paths to git projects and various binaries
################################################################################

LINUX_PATH      ?= $(CURDIR)/../linux-6.6.35
# LINUX_PATH      ?= ~/Homework/uefi-project/linux
LINUX_IMAGE     ?= $(LINUX_PATH)/arch/x86_64/boot/bzImage

linux:
	make -C $(LINUX_PATH) -j16 

linux-clean:
	make clean -C $(LINUX_PATH)

################################################################################
# Qemu run
################################################################################

run:
	qemu-system-x86_64  \
	  -S -s \
	  -smp 4 \
	  -kernel $(LINUX_IMAGE) \
	  -initrd $(CURDIR)/initramfs-busybox-x64.cpio.gz \
	  -nographic \
	  --append "root=/dev/ram init=/init console=ttyS0 nokaslr" \
	  -m 512M

run-only:
	qemu-system-x86_64  \
	  -smp 4 \
	  -kernel $(LINUX_IMAGE) \
	  -initrd $(CURDIR)/initramfs-busybox-x64.cpio.gz \
	  -nographic \
	  --append "root=/dev/ram init=/init console=ttyS0 nokaslr" \
	  -m 512M
