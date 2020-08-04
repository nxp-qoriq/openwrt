#
# Copyright 2020 NXP
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=nfc-module
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=ssh://git@bitbucket.sw.nxp.com/dash/nfc-module.git
PKG_SOURCE_VERSION:=7ba10c7a51a00cc3edd269bdf5c10b14618a6def
PKG_MIRROR_HASH:=3d5e2bc37d55b0e63aed41e86dcc77be24688cf1ace076fe50925bf15c4b54f8

include $(INCLUDE_DIR)/package.mk

define KernelPackage/nfc-module
  SUBMENU:=NFC support
  TITLE:=NXP nfc module
  FILES:=$(PKG_BUILD_DIR)/pn5xx_i2c.ko
  AUTOLOAD:=$(call AutoLoad,34,pn5xx_i2c)
endef

define KernelPackage/nfc-module/description
 Kernel module to support nfc.
endef

MAKE_OPTS:= \
	M="$(PKG_BUILD_DIR)"

define Build/Compile
	$(KERNEL_MAKE) KERNEL_DIR=$(LINUX_DIR) $(MAKE_OPTS) modules
endef

$(eval $(call KernelPackage,nfc-module))
