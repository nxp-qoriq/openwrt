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

ifeq ($(SUBTARGET),armv8_64b)
include armv8_64b.mk
endif

ifeq ($(SUBTARGET),armv8_32b)
include armv8_32b.mk
endif

ifeq ($(SUBTARGET),armv7)
include armv7.mk
endif

$(eval $(call BuildImage))
