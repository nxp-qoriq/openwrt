#
# Copyright 2020 NXP
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openthread
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=ssh://git@bitbucket.sw.nxp.com/dnnpi/ls1046awrdb-openthread.git
PKG_SOURCE_VERSION:=ec723b933f2c08ef1c86b2d93c819c40196f2290
PKG_MIRROR_HASH:=8abe9d3569bbf624eee22d22aae0249d616323ab24274495df91ff25caf50ad9

include $(INCLUDE_DIR)/package.mk

define Package/openthread
	SECTION:=base
	CATEGORY:=Network
	TITLE:=OpenThread
	DEPENDS:= +jn5189-programmer +otbr
endef

define Package/openthread/description
	An open-source implementation of the Thread networking protocol.
endef

define Build/Configure
	@echo "Build/Configure"
	sudo apt install -y python-pip
	pip install --upgrade pip
	pip install pycrypto pycryptodome
	cd $(PKG_BUILD_DIR) && ./script/bootstrap && ./bootstrap
endef

define Build/Compile
	@echo "Build/Compile"
	cd $(PKG_BUILD_DIR) && $(MAKE) -f src/posix/Makefile-posix clean && \
	HOST=$(REAL_GNU_TARGET_NAME) $(MAKE_VARS) READLINE=no $(MAKE) -f src/posix/Makefile-posix DAEMON=1 && \
	cd $(PKG_BUILD_DIR) && $(MAKE) -f examples/Makefile-jn5189 BORDER_AGENT=1 BORDER_ROUTER=1
	cd $(PKG_BUILD_DIR) && $(MAKE) -f examples/Makefile-jn5189 JOINER=1
endef

define Package/openthread/install
	@echo "Package/openthread/install"
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/firmware
	cd $(PKG_BUILD_DIR) && $(INSTALL_BIN) `find ./output -iname ot-ctl` $(1)/usr/bin
	cd $(PKG_BUILD_DIR) && $(INSTALL_BIN) `find ./output/jn5189 -iname ot-rcp.bin` $(1)/usr/firmware
	cd $(PKG_BUILD_DIR) && $(INSTALL_BIN) `find ./output/jn5189 -iname ot-cli-ftd.bin` $(1)/usr/firmware
endef

$(eval $(call BuildPackage,openthread))
