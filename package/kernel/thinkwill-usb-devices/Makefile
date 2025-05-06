# SPDX-License-Identifier: GPL-2.0
include $(TOPDIR)/rules.mk

PKG_NAME:=thinkwill-usb-devices
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/thinkwill-usb-devices
  SUBMENU:=USB Support
  TITLE:=Driver for ThinkWill ML7820 Series Devices
  DEPENDS:= \
    @USB_SUPPORT \
    +kmod-usb-net \
    +kmod-usb-net-cdc-ether \
    +kmod-usb-net-rndis \
    +kmod-usb-serial
  FILES:= \
    $(PKG_BUILD_DIR)/thinkwill-usb-devices.ko
  AUTOLOAD:=$(call AutoProbe,thinkwill-usb-devices)
endef

define KernelPackage/thinkwill-usb-devices/description
  Kernel module for ThinkWill ML7820 series USB devices
  Supports ECM/NDIS/Download modes
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		M="$(PKG_BUILD_DIR)" \
		modules
endef

define KernelPackage/thinkwill-usb-devices/install
	$(INSTALL_DIR) $(1)/etc/modules.d
	echo "thinkwill-usb-devices" > $(1)/etc/modules.d/90-thinkwill-usb-devices
endef

$(eval $(call KernelPackage,thinkwill-usb-devices))