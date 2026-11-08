# SPDX-License-Identifier: GPL-2.0-only
#
# A LuCI package of hardware info.
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI status for hardware include NSS offloading
LUCI_DESCRIPTION:=Hardwareinfo Status ECM acceleration counts, SQM and fast-lane health), and \
 adds the NSS core load and the ECM-accelerated connections to Status -> Overview.
LUCI_DEPENDS:=+luci-base
LUCI_PKGARCH:=all

PKG_LICENSE:=GPL-2.0-only

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
