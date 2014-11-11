#
# Copyright (C) 2014-2015 BalaBit IT Security
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=kzorp
PKG_VERSION:=6.0.0

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/balabit/kzorp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE_VERSION:=3c6d9390edade81f8aee822d5cf07451ea9cf34e
PKG_SOURCE_PROTO:=git

PKG_FIXUP:=autoreconf
PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_INSTALL:=1

PKG_MAINTAINER:=Szil√rd Pfeiffer <coroner@balabit.hu>

include $(INCLUDE_DIR)/package.mk

define KernelPackage/kernel-zorp/Default
  SECTION:=kernel
  CATEGORY:=Kernel modules
  SUBMENU:=Zorp Firewall
  BUILD_DEPENDS:= kmod-ipt-conntrack +kmod-ipt-core +kmod-ipt-nat +kmod-ipt-tproxy +kmod-nfnetlink
endef
#AUTOLOAD:=$(call AutoLoad,30,wl_glue wl)

define KernelPackage/kzorp
$(call KernelPackage/kernel-zorp/Default,)
  TITLE:=Netfilter kZorp support
  DEPENDS:= +kmod-ipv6 +kmod-nf-nat +kmod-x-tables +kmod-ip6tables
  FILES:=$(PKG_BUILD_DIR)/driver/kzorp.ko
endef

define KernelPackage/kzorp-target
$(call KernelPackage/kernel-zorp/Default,)
  TITLE:=kZorp target support
  DEPENDS:= +kmod-kzorp
  FILES:=$(PKG_BUILD_DIR)/driver/xt_KZORP.ko
endef

define KernelPackage/kzorp-socket-match
$(call KernelPackage/kernel-zorp/Default,)
  TITLE:=kZorp socket match
  DEPENDS:= +kmod-kzorp
  FILES:=$(PKG_BUILD_DIR)/driver/xt_socket_kzorp.ko
endef

define KernelPackage/service-match
$(call KernelPackage/kernel-zorp/Default,)
  TITLE:=kZorp service match
  DEPENDS:= +kmod-kzorp
  FILES:=$(PKG_BUILD_DIR)/driver/xt_service.ko
endef

define KernelPackage/zone-match
$(call KernelPackage/kernel-zorp/Default,)
  TITLE:=kZorp zone match
  DEPENDS:= +kmod-kzorp
  FILES:=$(PKG_BUILD_DIR)/driver/xt_zone.ko
endef

define Package/kzorp
	CATEGORY:=Network
	SUBMENU:=Firewall
	TITLE:=kzorp
	DEPENDS:= +python +python-daemon +python-prctl +python-radix +pydns +kmod-kzorp +kmod-kzorp-target +kmod-service-match +kmod-kzorp-socket-match
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(PKG_BUILD_DIR)/driver" \
	EXTRA_CFLAGS="-I$(PKG_BUILD_DIR)/driver/include"

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/usr --root=$(PKG_INSTALL_DIR))
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) -- \
		KBUILD="$(LINUX_DIR)"
endef

PYTHON_PKG_DIR:=/usr/lib/python2.7/site-packages

define Package/kzorp/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/sbin/kzorp-client \
		$(PKG_INSTALL_DIR)/usr/sbin/kzorpd \
		$(1)/usr/sbin

	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/kzorp
	$(CP) $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/kzorp/* \
		$(1)$(PYTHON_PKG_DIR)/kzorp

	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)/Zorp
	$(CP) $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/Zorp/* \
		$(1)$(PYTHON_PKG_DIR)/Zorp

	$(INSTALL_DIR) $(1)/lib/modules/3.10$(LINUX_VERSION-3.10)
	$(CP) $(PKG_BUILD_DIR)/driver/*.ko \
		$(1)/lib/modules/3.10$(LINUX_VERSION-3.10)
endef

$(eval $(call KernelPackage,kzorp))
$(eval $(call KernelPackage,kzorp-target))
$(eval $(call KernelPackage,kzorp-socket-match))
$(eval $(call KernelPackage,service-match))
$(eval $(call KernelPackage,zone-match))
$(eval $(call BuildPackage,kzorp))
