#
# Copyright (C) 2006-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#


include $(TOPDIR)/rules.mk

PKG_NAME:=hisi-osdrv3
PKG_VERSION:=3.18.20
PKG_RELEASE:=1.0.4.0

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=HISILICON COPYING

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/default
	SECTION:=openipc
	CATEGORY:=OpenIPC
	MAINTAINER:=Igor Zalatov <flyrouter@gmail.com>
	TITLE:=Hisilicon OSDRV-3
	SUBMENU:=HiSilicon related
	URL:=http://zftlab.org
	DEPENDS:=@(TARGET_hi35xx_16cv300||TARGET_hi35xx_16ev100)
endef

define Package/$(PKG_NAME)/Default/description
	Hisilicon OSDRV kernel modules, drivers and libs
endef

define Package/$(PKG_NAME)-base
$(call Package/$(PKG_NAME)/default)
	TITLE+= - base package
endef

define Package/$(PKG_NAME)-binary
$(call Package/$(PKG_NAME)/default)
	TITLE+= - binary package
	DEPENDS:=+$(PKG_NAME)-lib +libpthread +libevent2 +lame-lib
endef

define Package/$(PKG_NAME)-kmod
$(call Package/$(PKG_NAME)/default)
	TITLE+= - kmod package
endef

define Package/$(PKG_NAME)-lib
$(call Package/$(PKG_NAME)/default)
	TITLE+= - lib package
endef

define Package/$(PKG_NAME)-sensor
$(call Package/$(PKG_NAME)/default)
	TITLE+= - binary sensor package
	DEPENDS:=+libstdcpp
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/$(PKG_NAME)
	$(CP) ./include/* $(STAGING_DIR)/usr/include/$(PKG_NAME)/
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) ./lib/*.so $(STAGING_DIR)/usr/lib/
endef

define Package/$(PKG_NAME)-base/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./script/* $(1)/usr/bin/
endef

define Package/$(PKG_NAME)-binary/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./script/ipcam.init $(1)/etc/init.d/ipcam
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./binary/bin/* $(1)/usr/bin/
	$(CP) ./script/ircut_demo $(1)/usr/bin/
	$(INSTALL_BIN) ./script/load_hisilicon $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/sensors
	$(CP) ./binary/etc/sensors/* $(1)/etc/sensors/
	$(CP) ./binary/etc/minihttp.ini $(1)/etc/
	$(INSTALL_DIR) $(1)/usr/lib/fonts
	$(CP) ./binary/lib/fonts/* $(1)/usr/lib/fonts/
	$(INSTALL_DIR) $(1)/usr/lib/sensors
	$(CP) ./binary/lib/sensors/*.so $(1)/usr/lib/sensors/
endef

define Package/$(PKG_NAME)-kmod/install
	$(INSTALL_DIR) $(1)/lib/modules/$(PKG_VERSION)
	$(CP) ./kmod/*.ko $(1)/lib/modules/$(PKG_VERSION)
endef

define Package/$(PKG_NAME)-lib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) ./lib/lib*.so $(1)/usr/lib/
endef

define Package/$(PKG_NAME)-sensor/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) ./sensor/libsns_*.so $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/etc/sensors
	$(CP) ./sensor/config/* $(1)/etc/sensors
endef

$(eval $(call BuildPackage,$(PKG_NAME)-base))
$(eval $(call BuildPackage,$(PKG_NAME)-binary))
$(eval $(call BuildPackage,$(PKG_NAME)-kmod))
$(eval $(call BuildPackage,$(PKG_NAME)-lib))
$(eval $(call BuildPackage,$(PKG_NAME)-sensor))
