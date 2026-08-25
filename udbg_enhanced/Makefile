include $(TOPDIR)/rules.mk

PKG_NAME:=udbg-enhanced
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=QCA
  CATEGORY:=qca-wifi-apps
  TITLE:=Udebug Enhanced
endef

define Package/$(PKG_NAME)/description
  Alternative to exisitng Udebug framework. This infrastructure is intended
  to be leveraged by hostapd/wpa_supplicant for lof diagonistic log collection.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -r $(TOPDIR)/qca/src/qca-wifi-apps/udbg_enh/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) clean
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -Iinc -fPIC" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/udbg_enh/client
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/client/inc/*.h $(1)/usr/include/udbg_enh/client/
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/client/libudbg_client_core.so $(1)/usr/lib/
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/udbg_enh_server $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/udbg_enh_server_cli $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/client/libudbg_client_core.so $(1)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
