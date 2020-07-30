#
# Copyright 2020 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libnfc-nci
PKG_VERSION:=R2.4-fix
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=ssh://git@bitbucket.sw.nxp.com/dnnpi/libnfc-nci.git
PKG_SOURCE_VERSION:=30d4b309737c2bd214cbe3035f39eb7e96116cd6
PKG_MIRROR_HASH:=42506a5d5121bf814b9d148e5abe77b8b2bb35d30a66b82fc628b871e3b64e48

PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/libnfc-nci
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Linux NFC stack for NCI based NXP NFC Controllers
  DEPENDS:=@TARGET_layerscape +libyaml +libpthread +libc +libstdcpp +openthread +otbr +kmod-nfc-module
endef

define Package/libnfc-nci/description
  Linux NFC stack for NCI based NXP NFC Controllers,
  provide a user space application to add an end device
  to thread network with nfc(thread commissioning with nfc)
endef

define Build/Configure
	@echo "Build/Configure"
	cd $(PKG_BUILD_DIR) && ./bootstrap
	cd $(PKG_BUILD_DIR) && HOST=$(REAL_GNU_TARGET_NAME) ./configure \
		--host=$(REAL_GNU_TARGET_NAME) CXX=$(TARGET_CROSS)g++
endef

define Package/libnfc-nci/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/local/etc
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) $(PKG_BUILD_DIR)/.libs/libnfc_nci_linux.so $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/.libs/libnfc_nci_linux-1.so $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/.libs/nfcDemoApp $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/conf/* $(1)/usr/local/etc/
	$(CP) $(PKG_BUILD_DIR)/openwrt/nfc $(1)/etc/init.d
endef

$(eval $(call BuildPackage,libnfc-nci))
