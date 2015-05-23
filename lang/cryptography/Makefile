#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cryptography
PKG_VERSION:=0.2.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/c/cryptography/
PKG_MD5SUM:=f002a442c8c5c7463bf8d2f11f6c3128

PKG_LICENSE:=Apache
PKG_MAINTAINER:=Szilard Pfeiffer <coroner@balabit.hu>

PKG_BUILD_DEPENDS:=six

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/cryptography
	SECTION:=lang-python
	CATEGORY:=Languages
	SUBMENU:=Python
	TITLE:=cryptography
	URL:=https://pypi.python.org/pypi/cryptography
	DEPENDS:=+python +libopenssl
endef

define Package/cryptography/description
Six is a Python 2 and 3 compatibility library. It provides utility functions
for smoothing over the differences between the Python versions with the goal
of writing Python code that is compatible on both Python versions. See the
documentation for more information on what is provided.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/cryptography/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,cryptography))
