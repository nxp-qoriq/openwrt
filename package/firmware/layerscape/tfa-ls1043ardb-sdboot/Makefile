#
# Copyright 2019 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=tfa-ls1043ardb-sdboot
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
	PLAT=ls1043ardb \
	BOOT_MODE=sd \
	RCW=$(STAGING_DIR_IMAGE)/ls1043ardb-sdboot-rcw.bin \
	BL33=$(STAGING_DIR_IMAGE)/ls1043ardb-sdboot-uboot.bin

define Package/tfa-ls1043ardb-sdboot
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_layerscape +u-boot-ls1043ardb-sdboot +layerscape-rcw-ls1043ardb-sdboot

  TITLE:=NXP LS1043ARDB TF-A SD boot
  GENERATED_DIR:=build/ls1043ardb/release
endef


define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/$(GENERATED_DIR)/bl2_sd.pbl $(STAGING_DIR_IMAGE)/ls1043ardb-sdboot-bl2.pbl
	$(CP) $(PKG_BUILD_DIR)/$(GENERATED_DIR)/fip.bin $(STAGING_DIR_IMAGE)/ls1043ardb-sdboot-fip.bin
endef

define Package/tfa-ls1043ardb-sdboot/install
endef

$(eval $(call BuildPackage,tfa-ls1043ardb-sdboot))

