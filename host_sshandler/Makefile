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
	Host subsystem handler for Debug Agent to process ath12k UIO interrupt/data buffers,
	Netlink buffers, event handling and trigger diagnostic actions.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -r $(TOPDIR)/qca/src/qca-wifi-apps/host_sshandler/* $(PKG_BUILD_DIR)/
endef

DA_INCLUDE := $(TOPDIR)/../da/gwapps_da_libs_bins/include
TC_INCLUDE := $(TOPDIR)/../frmwrk/gwapps_cmn_headers/transport_lib

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -I. -I$(DA_INCLUDE) -I$(TC_INCLUDE) -fPIC" \
		LDFLAGS="$(TARGET_LDFLAGS) -lpthread -shared"
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libhost_subsystem_handler.so $(1)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
