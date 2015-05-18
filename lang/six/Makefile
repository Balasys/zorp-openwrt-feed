#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=six
PKG_VERSION:=1.9.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/s/six/
PKG_MD5SUM:=476881ef4012262dfc8adc645ee786c4

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Szilard Pfeiffer <coroner@balabit.hu>

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/six
	SECTION:=lang-python
	CATEGORY:=Languages
	SUBMENU:=Python
	TITLE:=six
	URL:=https://pypi.python.org/pypi/six
	DEPENDS:=+python +libcap
endef

define Package/six/description
Six is a Python 2 and 3 compatibility library. It provides utility functions
for smoothing over the differences between the Python versions with the goal
of writing Python code that is compatible on both Python versions. See the
documentation for more information on what is provided.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/six/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,six))
