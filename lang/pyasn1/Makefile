#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyasn1
PKG_VERSION:=0.1.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/source/p/pyasn1/
PKG_MD5SUM:=322b86d0c50a7d165c05600154cecc0a

PKG_LICENSE:=BSD
PKG_MAINTAINER:=Szilard Pfeiffer <coroner@balabit.hu>

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/pyasn1
	SECTION:=lang-python
	CATEGORY:=Languages
	SUBMENU:=Python
	TITLE:=pyasn1
	URL:=https://pypi.python.org/pypi/pyasn1
	DEPENDS:=+python
endef

define Package/pyasn1/description
Implementation of ASN.1 types and codecs in Python programming language. It
has been first written to support particular protocol (SNMP) but then
generalized to be suitable for a wide range of protocols based on ASN.1
specification.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
endef

define Package/pyasn1/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,pyasn1))
