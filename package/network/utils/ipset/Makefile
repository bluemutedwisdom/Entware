
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ipset
PKG_VERSION:=6.38
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://ipset.netfilter.org
PKG_HASH:=ceef625ba31fe0aaa422926c7231a819de0b07644c02c17ebdd3022a29e3e244

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>
PKG_LICENSE:=GPL-2.0

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ipset/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS+= +libmnl
  TITLE:=IPset administration utility
  URL:=http://ipset.netfilter.org/
endef

define Package/ipset
$(call Package/ipset/Default)
  DEPENDS+= +libipset
endef

define Package/libipset
$(call Package/ipset/Default)
endef

CONFIGURE_ARGS += \
	--with-kbuild="$(LINUX_DIR)" --with-kmod=no

MAKE_FLAGS += \
	ARCH="$(LINUX_KARCH)" \
	SHELL="$(BASH)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/include/libipset $(1)/opt/include/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libipset.{a,so*} $(1)/opt/lib/
	$(CP) $(PKG_BUILD_DIR)/lib/libipset.pc $(1)/opt/lib/pkgconfig/
endef

define Package/ipset/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/ipset $(1)/opt/sbin/
endef

define Package/libipset/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libipset*.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,ipset))
$(eval $(call BuildPackage,libipset))
