#
# Copyright (C) 2026 Wenjw
#
# This is free software, licensed under the Apache License, Version 2.0.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-rebootschedule
PKG_VERSION:=1.0.0
PKG_RELEASE:=1
PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=Wenjw <wenjw@example.com>

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-rebootschedule
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=LuCI support for scheduled reboot
  DEPENDS:=+luci-base
  PKGARCH:=all
endef

define Package/luci-app-rebootschedule/description
 Reboot this device automatically on a daily, weekly or uptime-interval
 schedule, configurable from LuCI.
endef

# 纯脚本包：没有任何需要编译的源码
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/luci-app-rebootschedule/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/usr/libexec/rebootschedule
	$(INSTALL_DIR) $(1)/usr/share/luci/menu.d
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/rebootschedule

	$(INSTALL_CONF) ./root/etc/config/rebootschedule $(1)/etc/config/rebootschedule
	$(INSTALL_BIN) ./root/etc/init.d/rebootschedule $(1)/etc/init.d/rebootschedule
	$(INSTALL_BIN) ./root/usr/libexec/rebootschedule/daemon $(1)/usr/libexec/rebootschedule/daemon
	$(INSTALL_DATA) ./root/usr/share/luci/menu.d/luci-app-rebootschedule.json $(1)/usr/share/luci/menu.d/
	$(INSTALL_DATA) ./root/usr/share/rpcd/acl.d/luci-app-rebootschedule.json $(1)/usr/share/rpcd/acl.d/
	$(INSTALL_DATA) ./htdocs/luci-static/resources/view/rebootschedule/overview.js \
		$(1)/www/luci-static/resources/view/rebootschedule/overview.js
endef

$(eval $(call BuildPackage,luci-app-rebootschedule))
