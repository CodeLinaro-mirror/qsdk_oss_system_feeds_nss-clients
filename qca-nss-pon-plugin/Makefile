include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=qca-nss-pon-plugin
PKG_SOURCE_PROTO:=git
PKG_BRANCH:=master
PKG_RELEASE:=1

LOCAL_SRC:=$(TOPDIR)/qca/src/nss/clients/qca-nss-pon-plugin

include $(INCLUDE_DIR)/local-development.mk
ifeq ($(DUMP)$(PKG_VERSION),)
  PKG_VERSION:=$(shell git ls-remote $(PKG_SOURCE_URL) $(PKG_BRANCH) | cut -b -7)
endif

include $(INCLUDE_DIR)/package.mk

define KernelPackage/qca-nss-pon-plugin
  SECTION:=kernel
  CATEGORY:=Kernel modules
  SUBMENU:=Network Devices
  TITLE:=Kernel driver for PON plugin
  DEPENDS:=@TARGET_ipq52xx
  FILES:=$(PKG_BUILD_DIR)/qca-nss-pon-plugin.ko
endef

define KernelPackage/qca-nss-pon-plugin/Description
Kernel module mediating between the ECM and PON/OMCI drivers without
either depending directly on the other.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/qca-nss-pon-plugin
	$(CP) $(PKG_BUILD_DIR)/exports/* $(1)/usr/include/qca-nss-pon-plugin/
endef

EXTRA_CFLAGS += -I$(PKG_BUILD_DIR)/exports

MAKE_OPTS+=qca-nss-pon-plugin=m

define Build/Compile
	$(KERNEL_MAKE) $(strip $(MAKE_OPTS)) \
		M="$(PKG_BUILD_DIR)" \
		EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
		modules
endef

$(eval $(call KernelPackage,qca-nss-pon-plugin))
