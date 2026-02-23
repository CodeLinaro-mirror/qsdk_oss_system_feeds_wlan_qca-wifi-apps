include $(TOPDIR)/rules.mk

PKG_NAME:=host-sshandler
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=QCA
  CATEGORY:=qca-wifi-apps
  TITLE:=Host Subsystem Handler
  DEPENDS:=+libpthread
endef

define Package/$(PKG_NAME)/description
  Daemon to monitor and copy UIO buffer data periodically sent from ath12k driver and trigger diagnostic action.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -r $(TOPDIR)/qca/src/qca-wifi-apps/host_sshandler/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -I." \
		LDFLAGS="$(TARGET_LDFLAGS) -lpthread"
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/host_sshandler $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
