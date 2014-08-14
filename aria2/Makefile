include $(TOPDIR)/rules.mk

PKG_NAME:=aria2
PKG_VERSION:=1.16.1
PKG_RELEASE:=1.16

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/aria2
PKG_MD5SUM:=ad7e0575ce4a480eb54030e1d348e076

include $(INCLUDE_DIR)/package.mk

define Package/aria2
	SECTION:=net
	CATEGORY:=Network
	DEFAULT:=y
	TITLE:=Aria2
	URL:=http://aria2.sourceforge.net
	DEPENDS:=+libopenssl +zlib +libstdcpp
endef

define Package/aria2/description
	Aria2
endef

TARGET_CFLAGS+=-fPIC 
TARGET_CXXFLAGS+=-fPIC
define Build/Compile
	$(call Build/Compile/Default, -f Makefile CFLAGS="$(TARGET_CFLAGS)")
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--prefix=/usr)
endef

define Package/aria2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/aria2c $(1)/usr/bin
endef

$(eval $(call BuildPackage,aria2))
