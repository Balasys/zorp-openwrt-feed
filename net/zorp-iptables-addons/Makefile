include $(TOPDIR)/rules.mk

# Name and release number of this package
PKG_NAME:=zorp-iptables-addons
PKG_VERSION:=1.0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/balabit/$(PKG_NAME).git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE_VERSION:=9b9de03eb685e2b40a29930a18d1b12b42bba0bc
PKG_SOURCE_PROTO:=git

PKG_LICENSE:=GPLv2

PKG_INSTALL:=1
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/zorp-iptables-addons
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Zorp IPTables addons
	DEPENDS:= +libxtables
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh)
	$(call Build/Configure/Default)
endef

define Package/zorp-iptables-addons/install
	$(INSTALL_DIR) $(1)/usr/lib/iptables
	$(CP) $(PKG_BUILD_DIR)/extensions/libxt_*.so $(1)/usr/lib/iptables/
endef

$(eval $(call BuildPackage,zorp-iptables-addons,+libxtables))
