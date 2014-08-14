include $(TOPDIR)/rules.mk

PKG_NAME:=jpeg
PKG_VERSION:=v6b
PKG_RELEASE:=6b

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_RELEASE)
PKG_SOURCE:=$(PKG_NAME)src.$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/libjpeg
PKG_MD5SUM:=dbd5f3b47ed13132f04c685d608a7547

include $(INCLUDE_DIR)/package.mk

define Package/jpeg
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=jpeg
	URL:=http://libjpeg.sourceforge.net
	DEPENDS:=+zlib
endef

define Package/jpeg/description
	JPEG C library
endef

TARGET_CFLAGS += -fPIC 
TARGET_CXXFLAGS += -fPIC
define Build/Compile
	$(call Build/Compile/Default, -f Makefile CFLAGS="$(TARGET_CFLAGS)")
endef

TARGET_AR += -acs
define Build/Configure
	$(call Build/Configure/Default, --prefix=/usr \
		--enable-static --enable-shared)
endef

define Package/jpeg/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/libjpeg.a $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/libjpeg.so* $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/libjpeg.so.* $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/jpeglib.h $(1)/usr/include/jpeglib.h
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/jconfig.h $(1)/usr/include/jconfig.h
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/jmorecfg.h $(1)/usr/include/jmorecfg.h
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/jerror.h $(1)/usr/include/jerror.h
endef

$(eval $(call BuildPackage,jpeg))
