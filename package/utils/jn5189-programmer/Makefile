#
# Copyright 2020 NXP
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jn5189-programmer
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=ssh://git@bitbucket.sw.nxp.com/dnnpi/ls1046awrdb-jmp.git
PKG_SOURCE_VERSION:=fb530d95576444091d464f735f8995eb4563b48d
PKG_MIRROR_HASH:=5d34bec390581f1b46dccccc879ee8f021f6eff60b93367a8d56299ff078e4bd

include $(INCLUDE_DIR)/package.mk

define Package/jn5189-programmer
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=jn5189/k32w061 flash programmer
  DEPENDS:=+libftdi +libusb-1.0 +libncurses +libgpiod +kmod-usb-serial +kmod-usb-serial-ftdi \
           +kmod-gpio-pca953x
endef

define Package/jn5189_programmer/description
  A flash programmer for jn5189/k32w061
endef

define Build/Configure
	@echo "Build/Configure"
endef

define Build/Compile
	@echo "Build/Compile"
	cd $(PKG_BUILD_DIR)/Library/Build && $(MAKE) clean
	cd $(PKG_BUILD_DIR)/CLI/Build && $(MAKE) clean
	cd $(PKG_BUILD_DIR)/CLI/Build && CC=$(TARGET_CROSS)gcc LD=$(TARGET_CROSS)ld $(MAKE) -j`nproc`
endef

define Package/jn5189-programmer/install
	$(INSTALL_DIR) $(1)/usr/local/sbin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/CLI/Build/DK6Programmer $(1)/usr/local/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/CLI/Build/flash-ot-rcp-firmware-to-jn5189.sh $(1)/usr/local/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/CLI/Build/openwrt/init.d/flash-ot-rcp-firmware-to-jn5189 $(1)/etc/init.d
endef

$(eval $(call BuildPackage,jn5189-programmer))
