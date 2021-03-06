#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vala
PKG_VERSION:=0.26.1
PKG_RELEASE:=1
PKG_LICENSE:=LGPL-2.1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/vala/0.26/
PKG_MD5SUM:=723a03b822d4cc47abc4019685970a3e

PKG_BUILD_DEPENDS:=glib2/host vala/host
HOST_BUILD_DEPENDS:=glib2/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

TARGET_LDFLAGS+=\
        -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Package/vala
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=C-sharp like language for the GObject system
  URL:=https://wiki.gnome.org/Projects/Vala
  MAINTAINER:=Gergely Kiss <mail.gery@gmail.com>
endef

define Package/vala/description
Vala is a C-sharp like language for the GObject system. This package contains
the Vala-to-C compiler.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Build/InstallDev
	$(INSTALL_DIR) \
		$(1)/usr/share/vala-0.26/vapi \
		$(1)/usr/lib \
		$(1)/usr/share/pkgconfig \
		$(1)/usr/bin

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/vala-0.26/vapi/* \
		$(1)/usr/share/vala-0.26/vapi

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/libvala-0.26.{so*,la} \
		$(1)/usr/lib

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/{vala,vala-0.26,valac,valac-0.26,vapicheck,vapicheck-0.26,vapigen,vapigen-0.26,vala-gen-introspect,vala-gen-introspect-0.26} \
		$(1)/usr/bin

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pkgconfig/*.pc \
		$(1)/usr/share/pkgconfig
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,vala))
