# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2022-2023 ImmortalWrt.org

include $(TOPDIR)/rules.mk

LUCI_TITLE:=The modern ImmortalWrt proxy platform for ARM64/AMD64
LUCI_PKGARCH:=all
LUCI_DEPENDS:= \
	+sing-box \
	+firewall4 \
	+kmod-nft-tproxy \
	+ucode-mod-digest

PKG_NAME:=luci-app-homeproxy-clashapi

define Package/luci-app-homeproxy-clashapi/conffiles
/etc/config/homeproxy
/etc/homeproxy/certs/
/etc/homeproxy/ruleset/
/etc/homeproxy/resources/direct_list.txt
/etc/homeproxy/resources/proxy_list.txt
endef

include $(TOPDIR)/feeds/luci/luci.mk

define Package/luci-app-homeproxy-clashapi/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./root/etc/init.d/homeproxy $(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./root/etc/config/homeproxy $(1)/etc/config/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./root/etc/uci-defaults/luci-homeproxy $(1)/etc/uci-defaults/
	$(INSTALL_BIN) ./root/etc/uci-defaults/luci-homeproxy-migration $(1)/etc/uci-defaults/

	$(INSTALL_DIR) $(1)/etc/homeproxy
	$(INSTALL_DIR) $(1)/etc/homeproxy/scripts
	$(INSTALL_DIR) $(1)/etc/homeproxy/resources
	$(INSTALL_DIR) $(1)/etc/homeproxy/ruleset
	$(INSTALL_DIR) $(1)/etc/homeproxy/certs
	$(INSTALL_DIR) $(1)/etc/acme

	$(INSTALL_BIN) ./root/etc/homeproxy/scripts/* $(1)/etc/homeproxy/scripts/

	$(INSTALL_CONF) ./root/etc/homeproxy/resources/direct_list.txt $(1)/etc/homeproxy/resources/
	$(INSTALL_CONF) ./root/etc/homeproxy/resources/proxy_list.txt $(1)/etc/homeproxy/resources/

	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DIR) $(1)/usr/share/rpcd
	$(INSTALL_DIR) $(1)/usr/share/rpcd/ucode
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d

	$(INSTALL_DATA) ./root/usr/share/rpcd/ucode/luci.homeproxy $(1)/usr/share/rpcd/ucode/
	$(INSTALL_DATA) ./root/usr/share/rpcd/acl.d/luci-app-homeproxy.json $(1)/usr/share/rpcd/acl.d/

	$(INSTALL_DIR) $(1)/usr/share/luci
	$(INSTALL_DIR) $(1)/usr/share/luci/menu.d
	$(INSTALL_DIR) $(1)/usr/share/luci/static/resources
	$(INSTALL_DIR) $(1)/usr/share/luci/static/resources/view/homeproxy

	$(INSTALL_DATA) ./root/usr/share/luci/menu.d/luci-app-homeproxy.json $(1)/usr/share/luci/menu.d/

	$(INSTALL_DATA) ./htdocs/luci-static/resources/homeproxy.js $(1)/usr/share/luci/static/resources/
	$(INSTALL_DATA) ./htdocs/luci-static/resources/view/homeproxy/*.js $(1)/usr/share/luci/static/resources/view/homeproxy/
endef

# call BuildPackage - OpenWrt buildroot signature
