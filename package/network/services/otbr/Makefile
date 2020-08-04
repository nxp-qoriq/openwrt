#
# Copyright 2020 NXP
#

include $(TOPDIR)/rules.mk

PKG_NAME:=otbr
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=ssh://git@bitbucket.sw.nxp.com/dnnpi/ls1046awrdb-ot-br-posix.git
PKG_SOURCE_VERSION:=8e122be66774415892ab415830f3810e680038df
PKG_MIRROR_HASH:=fe461c4a5325bcf4e97ab0460a0623662594a67ca9caded9aced86ce0f6748bd

include $(INCLUDE_DIR)/package.mk

define Package/otbr
	SECTION:=base
	CATEGORY:=Network
	TITLE:=OpenThread border router
	DEPENDS:=+libjson-c +libstdcpp +dbus +libreadline +boost +boost-system +tayga +libblobmsg-json +libubox +libubus
endef

define Package/otbr/description
	A mesh network border router implementation -application.
endef

CONFIGURE_ARGS += \
	--disable-docs \
	--disable-web-service \
	--enable-openwrt \
	--with-ncp=openthread \
	--with-mdns=none

MAKE_VARS += \
	HOST=$(REAL_GNU_TARGET_NAME)

TARGET_CPPFLAGS+= -I$(STAGING_DIR)/usr/include/dbus-1.0 \
		  -I$(STAGING_DIR)/usr/lib/dbus-1.0/include

TARGET_LDFLAGS+= -ldbus-1 -lpthread

define Build/Prepare
	$(Build/Prepare/Default)
	cd $(PKG_BUILD_DIR) && ./script/bootstrap
endef

define Package/otbr/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller/admin
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view
	$(INSTALL_DIR) $(1)/www/luci-static/resources
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/agent/otbr-agent $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tools/pskc $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/openwrt/controller/thread.lua $(1)/usr/lib/lua/luci/controller/admin
	$(CP) $(PKG_BUILD_DIR)/src/openwrt/view/admin_thread $(1)/usr/lib/lua/luci/view
	$(CP) $(PKG_BUILD_DIR)/src/openwrt/handle_error.js $(1)/www/luci-static/resources
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/openwrt/otbr $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/openwrt/init.d/set-ip-nat-of-nat64 $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/openwrt/uci-defaults/01-uci-set-nat64 $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/usr/lib
endef

$(eval $(call BuildPackage,otbr))
