#
# Copyright (C) 2016 Jiang Yutang <jiangyutang1978@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Build/ls-clean
	rm -f $@
endef

define Build/ls-append
	dd if=$(STAGING_DIR_IMAGE)/$(1) >> $@
endef

define Build/ls-append-dtb
	$(call Image/BuildDTB,$(DTS_DIR)/$(1).dts,$(DTS_DIR)/$(1).dtb)
	dd if=$(DTS_DIR)/$(1).dtb >> $@
endef

define Device/Default
  PROFILES = Default
  FILESYSTEMS := squashfs
  DEVICE_DTS :=
  IMAGES = firmware.bin

ifeq ($(SUBTARGET),armv8_64b)
  KERNEL := kernel-bin | gzip | uImage gzip
  KERNEL_LOADADDR = 0x80080000
  KERNEL_ENTRY_POINT = 0x80080000
endif
ifeq ($(SUBTARGET),armv8_32b)
  KERNEL := kernel-bin | uImage none
  KERNEL_NAME := zImage
  KERNEL_LOADADDR = 0x80008000
  KERNEL_ENTRY_POINT = 0x80008000
endif
endef

define Device/ls1043ardb
  DEVICE_TITLE := ls1043ardb-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls1043ardb layerscape-fman-ls1043ardb \
			layerscape-ppa-ls1043ardb
  ifeq ($(SUBTARGET),armv8_32b)
    DEVICE_PACKAGES += u-boot-ls1043ardb-image
  endif
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls1043a-rdb-sdk
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 9M | \
			ls-append $(1)-fman.bin | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-rootfs | pad-rootfs | check-size 67108865
endef
TARGET_DEVICES += ls1043ardb

define Device/ls1046ardb
  DEVICE_TITLE := ls1046ardb-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls1046ardb layerscape-fman-ls1046ardb \
			layerscape-ppa-ls1046ardb
  ifeq ($(SUBTARGET),armv8_32b)
    DEVICE_PACKAGES += u-boot-ls1046ardb-image
  endif
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls1046a-rdb-sdk
  FILESYSTEMS := ubifs
  UBIFS_OPTS := -m 1 -e 262016 -c 128
  UBINIZE_OPTS := -E 5
  BLOCKSIZE := 256KiB
  PAGESIZE := 1
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 9M | \
			ls-append $(1)-fman.bin | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-ubi | check-size 67108865
endef
TARGET_DEVICES += ls1046ardb

define Device/ls1012ardb
  DEVICE_TITLE := ls1012ardb-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls1012ardb layerscape-ppfe \
			layerscape-ppa-ls1012ardb kmod-ppfe
  ifeq ($(SUBTARGET),armv8_32b)
    DEVICE_PACKAGES += u-boot-ls1012ardb-image
  endif
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls1012a-rdb
  FILESYSTEMS := ubifs
  UBIFS_OPTS := -m 1 -e 262016 -c 128
  UBINIZE_OPTS := -E 5
  BLOCKSIZE := 256KiB
  PAGESIZE := 1
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 10M | \
			ls-append pfe.itb | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-ubi | check-size 67108865
endef
TARGET_DEVICES += ls1012ardb

define Device/ls1012afrdm
  DEVICE_TITLE := ls1012afrdm-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls1012afrdm layerscape-ppfe \
			layerscape-ppa-ls1012afrdm kmod-ppfe
  ifeq ($(SUBTARGET),armv8_32b)
    DEVICE_PACKAGES += u-boot-ls1012afrdm-image
  endif
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls1012a-frdm
  FILESYSTEMS := ubifs
  UBIFS_OPTS := -m 1 -e 262016 -c 128
  UBINIZE_OPTS := -E 5
  BLOCKSIZE := 256KiB
  PAGESIZE := 1
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 10M | \
			ls-append pfe.itb | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-ubi | check-size 67108865
endef
TARGET_DEVICES += ls1012afrdm

ifeq ($(SUBTARGET),armv8_64b)
define Device/ls1088ardb
  DEVICE_TITLE := ls1088ardb-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls1088ardb uboot-layerscape-$(SUBTARGET)-ls1088ardb \
			layerscape-mc-ls1088ardb layerscape-dpl-ls1088ardb restool \
			layerscape-ppa-ls1088ardb
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls1088a-rdb
  FILESYSTEMS := ubifs
  UBIFS_OPTS := -m 1 -e 262016 -c 128
  UBINIZE_OPTS := -E 5
  BLOCKSIZE := 256KiB
  PAGESIZE := 1
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 10M | \
			ls-append $(1)-mc.itb | pad-to 13M | \
			ls-append $(1)-dpl.dtb | pad-to 14M | \
			ls-append $(1)-dpc.dtb | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-ubi | check-size 67108865
endef
TARGET_DEVICES += ls1088ardb

define Device/ls2088ardb
  DEVICE_TITLE := ls2088ardb-$(SUBTARGET)
  DEVICE_PACKAGES +=	layerscape-rcw-ls2088ardb uboot-layerscape-$(SUBTARGET)-ls2088ardb \
			layerscape-mc-ls2088ardb layerscape-dpl-ls2088ardb restool \
			layerscape-ppa-ls2088ardb
  DEVICE_DTS = ../../../arm64/boot/dts/freescale/fsl-ls2088a-rdb
  IMAGE/firmware.bin =	ls-clean | \
			ls-append $(1)-rcw.bin | pad-to 1M | \
			ls-append $(1)-uboot.bin | pad-to 3M | \
			ls-append $(1)-uboot-env.bin | pad-to 4M | \
			ls-append $(1)-ppa.itb | pad-to 10M | \
			ls-append $(1)-mc.itb | pad-to 13M | \
			ls-append $(1)-dpl.dtb | pad-to 14M | \
			ls-append $(1)-dpc.dtb | pad-to 15M | \
			ls-append-dtb $$(DEVICE_DTS) | pad-to 16M | \
			append-kernel | pad-to 32M | \
			append-rootfs | pad-rootfs | check-size 67108865
endef
TARGET_DEVICES += ls2088ardb
endif

$(eval $(call BuildImage))
