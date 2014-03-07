include $(TOPDIR)/rules.mk

# Name and release number of this package
PKG_NAME:=libzorpll
PKG_VERSION:=6.0.0.0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/balabit/libzorpll.git
PKG_SOURCE_SUBDIR:=libzorpll
PKG_SOURCE_VERSION:=377f36dc52db8f26c94f6300f0b62d8316709504
PKG_SOURCE_PROTO:=git

PKG_LICENSE:=LGPLv2

PKG_INSTALL:=1
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libzorpll
	CATEGORY:=Libraries
	SUBMENU:=Firewall
	TITLE:=libzorpll
	DEPENDS:= +libstdcpp +glib2 +libopenssl +zlib +libcap
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh)
	$(call Build/Configure/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr
	$(CP) $(PKG_INSTALL_DIR)/usr/* $(1)/usr/
endef

define Package/libzorpll/install
	$(INSTALL_DIR) $(1)/usr
	$(CP) $(PKG_INSTALL_DIR)/usr/* $(1)/usr/
endef

$(eval $(call BuildPackage,libzorpll))
