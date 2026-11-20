#
# Copyright (C) 2026 Wenjw
#
# This is free software, licensed under the Apache License, Version 2.0.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-rebootschedule
PKG_VERSION:=1.0.0
PKG_RELEASE:=3
PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=Wenjw <wenjw@example.com>

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-rebootschedule
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=LuCI support for scheduled reboot
  # 杩欐槸涓函鑴氭湰鍖咃紝涓嶅啓 +luci-base 鏄晠鎰忕殑锛氬啓浜嗕細璁?buildroot 鍘荤紪璇?  # luci-base -> lucihttp锛岃€?SDK 鐨?staging 閲岀己 lua 澶存枃浠讹紝鏋勫缓鐩存帴宕┿€?  # luci-base 鍦ㄤ换浣曡浜?LuCI 鐨勭郴缁熶笂閮藉瓨鍦紝杩愯鏃朵笉闇€瑕侀澶栨媺鍙栥€?  PKGARCH:=all
endef

define Package/luci-app-rebootschedule/description
 Reboot this device automatically on a daily, weekly or uptime-interval
 schedule, configurable from LuCI.
endef

# 绾剼鏈寘锛氭病鏈変换浣曢渶瑕佺紪璇戠殑婧愮爜
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

# 瑁呭畬/鍗歌浇鍚庡繀椤绘竻 LuCI 鐨勮彍鍗曠紦瀛樺苟 reload rpcd锛屽惁鍒欐柊鑿滃崟涓嶄細鍑虹幇銆?# luci.mk 浼氳嚜鍔ㄧ敓鎴愯繖娈碉紝鏅€氬寘瀹氫箟寰楄嚜宸卞啓銆?define Package/luci-app-rebootschedule/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	rm -f /tmp/luci-indexcache.*
	rm -rf /tmp/luci-modulecache/
	/etc/init.d/rpcd reload 2>/dev/null
	/etc/init.d/rebootschedule enable 2>/dev/null
	/etc/init.d/rebootschedule start 2>/dev/null
	exit 0
}
endef

define Package/luci-app-rebootschedule/prerm
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	/etc/init.d/rebootschedule stop 2>/dev/null
	/etc/init.d/rebootschedule disable 2>/dev/null
	rm -f /tmp/luci-indexcache.*
	rm -rf /tmp/luci-modulecache/
	/etc/init.d/rpcd reload 2>/dev/null
	exit 0
}
endef

$(eval $(call BuildPackage,luci-app-rebootschedule))
