#
# Copyright (C) 2026 Wenjw
#
# This is free software, licensed under the Apache License, Version 2.0.
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI support for scheduled reboot
LUCI_DESCRIPTION:=Reboot this device automatically on a daily, weekly or \
	uptime-interval schedule, configurable from LuCI.
LUCI_DEPENDS:=+luci-base
LUCI_PKGARCH:=all
PKG_LICENSE:=Apache-2.0
PKG_MAINTAINER:=Wenjw <wenjw@example.com>

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
