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
	$(MAKE) $(PKG_JOBS) -C \
		$(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)"
endef

TARGET_AR += -acs
define Build/Configure
	@echo "$(PKG_INSTALL_DIR)" > /opt/working/test_jpeg.txt
	$(call Build/Configure/Default, prefix=$(PKG_INSTALL_DIR) \
		--enable-static --enable-shared)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/.libs/libjpeg.{a,so,so.62,so.62.0.0} $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/jpeglib.h $(1)/usr/include/jpeglib.h
	$(CP) $(PKG_BUILD_DIR)/jconfig.h $(1)/usr/include/jconfig.h
	$(CP) $(PKG_BUILD_DIR)/jmorecfg.h $(1)/usr/include/jmorecfg.h
	$(CP) $(PKG_BUILD_DIR)/jerror.h $(1)/usr/include/jerror.h
endef

define Package/jpeg/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/.libs/libjpeg.{a,so,so.62,so.62.0.0} $(1)/usr/lib
endef

$(eval $(call BuildPackage,jpeg))
