include $(TOPDIR)/rules.mk

PKG_NAME:=libexif
PKG_VERSION:=0.6.21
PKG_RELEASE:=0.6

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/libexif
PKG_MD5SUM:=9321c409a3e588d4a99d63063ef4bbb7

include $(INCLUDE_DIR)/package.mk

define Package/libexif
	CATEGORY:=Libraries
	TITLE:=libexif
	URL:=http://libexif.sourceforge.net
endef

define Package/libexif/description
	Libexif
endef

TARGET_CFLAGS += -fPIC 
TARGET_CXXFLAGS += -fPIC
define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && \
		CC=mipsel-linux-cc CFLAGS="-fPIC" \
		./configure \
		--prefix=/usr \
		--host=mipsel-linux
endef

define Package/libexif/installDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libexif $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libexif.{a,so,so.12,so.12.3.3} $(1)/usr/lib
endef

define Package/libexif/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libexif.{a,so,so.12,so.12.3.3} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libexif))
