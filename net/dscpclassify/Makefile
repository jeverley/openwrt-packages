#
# Copyright (C) 2025 Jack Everley
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dscpclassify
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/jeverley/$(PKG_NAME)
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=

PKG_MAINTAINER:=Jack Everley <jeverley.dev@outlook.com>
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/dscpclassify
  SECTION:=net
  CATEGORY:=Network
  TITLE:=DSCP classify service for use with SQM Scripts
  URL:=https://github.com/jeverley/dscpclassify
  DEPENDS:=+firewall4 +kmod-sched-ctinfo +sqm-scripts
  PKGARCH:=all
endef

define Package/dscpclassify/conffiles
/etc/config/dscpclassify
endef

define Package/dscpclassify/description
An nftables service for applying DSCP class to connections for use with the layer_cake_ct.qos SQM Script.
endef

define Package/dscpclassify/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/etc/config/dscpclassify $(1)/etc/config/dscpclassify

	$(INSTALL_DIR) $(1)/etc/dscpclassify.d
	$(INSTALL_DATA) ./files/etc/dscpclassify.d/main.nft $(1)/etc/dscpclassify.d/main.nft
	$(INSTALL_DATA) ./files/etc/dscpclassify.d/maps.nft $(1)/etc/dscpclassify.d/maps.nft
	$(INSTALL_DATA) ./files/etc/dscpclassify.d/verdicts.nft $(1)/etc/dscpclassify.d/verdicts.nft

	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_BIN) ./files/etc/hotplug.d/iface/21-dscpclassify $(1)/etc/hotplug.d/iface/21-dscpclassify

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/dscpclassify $(1)/etc/init.d/dscpclassify

	$(INSTALL_DIR) $(1)/usr/lib/sqm
	$(INSTALL_DATA) ./files/usr/lib/sqm/layer_cake_ct.qos $(1)/usr/lib/sqm/layer_cake_ct.qos
	$(INSTALL_DATA) ./files/usr/lib/sqm/layer_cake_ct.qos.help $(1)/usr/lib/sqm/layer_cake_ct.qos.help
endef

$(eval $(call BuildPackage,dscpclassify))

