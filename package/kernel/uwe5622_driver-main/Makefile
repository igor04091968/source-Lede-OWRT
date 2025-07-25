#obj-$(CONFIG_RK_WIFI_DEVICE_UWE5622) += unisocwcn/
#obj-$(CONFIG_WLAN_UWE5622)    += unisocwifi/
#obj-$(CONFIG_TTY_OVERY_SDIO)  += tty-sdio/

#UNISOCWCN_DIR := $(shell cd $(src)/unisocwcn/ && /bin/pwd)
#UNISOC_BSP_INCLUDE := $(UNISOCWCN_DIR)/include
#export UNISOC_BSP_INCLUDE

#UNISOC_FW_PATH_CONFIG := "/lib/firmware/uwe5622/"
#export UNISOC_FW_PATH_CONFIG
include $(TOPDIR)/rules.mk

PKG_NAME:=uwe5622
PKG_VERSION:=2024-04-13
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Ran-Thegoth/uwe5622.git
PKG_SOURCE_VERSION:=HEAD
PKG_MIRROR_HASH:=skip
PKG_SOURCE_SUBDIR:=src

include $(INCLUDE_DIR)/package.mk

define KernelPackage/uwe5622
  SUBMENU:=Wireless Drivers
  TITLE:=uwe5622 WiFi Driver
  FILES:=$(PKG_BUILD_DIR)/uwe5622.ko
  AUTOLOAD:=$(call AutoLoad,50,uwe5622)
endef

define Build/Prepare
  $(CP) -r $(PKG_SOURCE_DIR)/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
  $(MAKE) -C $(LINUX_DIR) \
    M=$(PKG_BUILD_DIR) \
    modules
endef

define Package/uwe5622/install
  $(INSTALL_DIR) $(1)/etc/modules.d
  $(INSTALL_DATA) ./files/uwe5622.conf $(1)/etc/modules.d/
endef

$(eval $(call KernelPackage,uwe5622))
