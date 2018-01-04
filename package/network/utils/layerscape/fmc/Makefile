#
# Copyright 2017 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fmc
PKG_VERSION:=lsdk-1903
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://source.codeaurora.org/external/qoriq/qoriq-components/fmc
PKG_SOURCE_VERSION:=c7576ab7fb6fb09b68ebc40531e5452fc89e5cd5
PKG_MIRROR_HASH:=638f8059fe36973e7dbde6b8aa690a343106f74b35804dc05c524b3d643cd6db

include $(INCLUDE_DIR)/package.mk

define Package/fmc
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=@TARGET_layerscape +libxml2 +tclap +fmlib +libstdcpp
  TITLE:=Layerscape Frame Manager Configuration Tool
endef

define Package/fmc/description
  The Frame Manager Configuration tool is a software package whose
  primary purpose is converting Parse-Classify-Police-Distribute
  (PCD) descriptions of network packets flow into hardware
  configuration.
endef

MAKE_FLAGS += \
	-C source \
	FMD_USPACE_HEADER_PATH="$(STAGING_DIR)/include/fmd" \
	FMD_USPACE_LIB_PATH="$(STAGING_DIR)/lib" \
	LIBXML2_HEADER_PATH="$(STAGING_DIR)/usr/include/libxml2" \
	TCLAP_HEADER_PATH="$(STAGING_DIR)/usr/include"

define Package/fmc/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/source/fmc $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/
	$(CP) $(PKG_BUILD_DIR)/etc/* $(1)/etc/
endef

$(eval $(call BuildPackage,fmc))
