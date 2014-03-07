#
# Copyright (C) 2014-2015 BalaBit IT Security
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=zorp
PKG_VERSION:=6.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/balabit/zorp.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=6.0

PKG_MAINTAINER:=Szilárd Pfeiffer <coroner@balabit.hu>
PKG_LICENSE:=GPL-2.0

PKG_FIXUP:=./autogen.sh

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include/zorp -std=c++11 -fPIC
TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib -pthread -lz

include $(INCLUDE_DIR)/package.mk

define Package/zorp/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
endef

define Package/zorp
$(call Package/zorp/Default,)
  TITLE:=Zorp application level firewall
  DEPENDS:= +libstdcpp +glib2 +libopenssl +libpthread +python +libzorpll +python-radix +pydns +python-openssl +kzorp
endef

define Build/Configure
	$(call Build/Configure/Default,--with-pidfiledir=/var/run)
endef

define Package/zorp/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/etc/iproute2
	touch $(1)/etc/iproute2/group
	$(CP) $(PKG_INSTALL_DIR)/usr/* $(1)/usr/
	$(CP) $(PKG_INSTALL_DIR)/etc/* $(1)/etc/
endef

$(eval $(call BuildPackage,zorp))
