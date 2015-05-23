#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pycparser
PKG_VERSION:=2.13
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/p/pycparser/
PKG_MD5SUM:=e4fe1a2d341b22e25da0d22f034ef32f

PKG_LICENSE:=BSD
PKG_MAINTAINER:=Szilard Pfeiffer <coroner@balabit.hu>

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/pycparser
	SECTION:=lang-python
	CATEGORY:=Languages
	SUBMENU:=Python
	TITLE:=pycparser
	URL:=https://pypi.python.org/pypi/pycparser
	DEPENDS:=+python
endef

define Package/pycparser/description
Complete parser of the C language, written in pure Python using the PLY
parsing library. It parses C code into an AST and can serve as a front-end for
C compilers or analysis tools.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/pycparser/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,pycparser))
