#
# Copyright 2017 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fmc-eth-config
PKG_VERSION:=lsdk-1806
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://source.codeaurora.org/external/qoriq/qoriq-components/eth-config
PKG_SOURCE_VERSION:=eefb06353c8c3db34d22c26825b66e921bce617d
PKG_MIRROR_HASH:=c766f34791cbe8a375f6a8c3c4c8d0366acd64ab3ca8b09910a85f792b14b8c2

include $(INCLUDE_DIR)/package.mk

define Package/fmc-eth-config
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=@TARGET_layerscape
  TITLE:=Layerscape Ethernet Configuration Files
endef

define Build/Compile
endef

define Package/fmc-eth-config/install
	$(INSTALL_DIR) $(1)/etc/fmc/config/
	$(CP) $(PKG_BUILD_DIR)/obsolete $(1)/etc/fmc/config/
	$(CP) $(PKG_BUILD_DIR)/private $(1)/etc/fmc/config/
	$(CP) $(PKG_BUILD_DIR)/shared_mac $(1)/etc/fmc/config/
endef

$(eval $(call BuildPackage,fmc-eth-config))
