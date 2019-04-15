#
# Copyright 2019 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=tfa-ls2088ardb
PKG_VERSION:=lsdk-1903
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://source.codeaurora.org/external/qoriq/qoriq-components/atf
PKG_SOURCE_VERSION:=7e34aebe658c7c3439d2d68b0ce6b9776e8e6996
PKG_MIRROR_HASH:=b4efd8904548bd569fd799d76ab9315202c18583f8388957aa76f0a57877f762

include $(INCLUDE_DIR)/package.mk
export GCC_HONOUR_COPTS=s

MAKE_VARS = \
	CROSS_COMPILE="$(TARGET_CROSS)"

MAKE_FLAGS += \
	all \
	fip \
	pbl \
	PLAT=ls2088ardb \
	BOOT_MODE=nor \
	RCW=$(STAGING_DIR_IMAGE)/ls2088ardb-rcw.bin \
	BL33=$(STAGING_DIR_IMAGE)/ls2088ardb-uboot.bin

define Package/tfa-ls2088ardb
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_layerscape +u-boot-ls2088ardb +layerscape-rcw-ls2088ardb
  TITLE:=NXP LS1012ARDB TF-A
  GENERATED_DIR:=build/ls2088ardb/release
endef


define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/$(GENERATED_DIR)/bl2_nor.pbl $(STAGING_DIR_IMAGE)/ls2088ardb-bl2.pbl
	$(CP) $(PKG_BUILD_DIR)/$(GENERATED_DIR)/fip.bin $(STAGING_DIR_IMAGE)/ls2088ardb-fip.bin
endef

define Package/tfa-ls2088ardb/install
endef

$(eval $(call BuildPackage,tfa-ls2088ardb))

