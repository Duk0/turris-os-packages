#
## Copyright (C) 2017 CZ.NIC z.s.p.o. (http://www.nic.cz/)
#
## This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# #
#
include $(TOPDIR)/rules.mk

PKG_NAME:=pakon-guts
PKG_VERSION:=4.1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.labs.nic.cz/turris/pakon-guts.git
PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_MAINTAINER:=Michal Vaner <michal.vaner@nic.cz>
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/pakon-guts
	TITLE:=pakon-guts
	DEPENDS:=+liblua +libnetfilter-queue +iptables-mod-nfqueue +libstdcpp
endef

define Build/Compile
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) NO_DOC=1 RELEASE=1 MAX_LOG_LEVEL=DBG
endef

define Package/pakon-guts/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/libpakond.so $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/pakond $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pakon_wrapper.sh $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pakon.init $(1)/etc/init.d/pakond

	$(INSTALL_DIR) $(1)/etc/firewall.d/with_reload
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pakon.fw $(1)/etc/firewall.d/with_reload/99_pakon.fw

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/pakon.conf $(1)/etc/config/pakon
endef

define Package/pakon-guts/conffiles
/etc/config/pakon
endef

$(eval $(call BuildPackage,pakon-guts))
