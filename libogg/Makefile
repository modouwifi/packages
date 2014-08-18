include $(TOPDIR)/rules.mk

PKG_NAME:=libogg
PKG_VERSION:=1.3.2
PKG_RELEASE:=1.3.2

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://downloads.xiph.org/releases/ogg
PKG_MD5SUM:=5c3a34309d8b98640827e5d0991a4015

include $(INCLUDE_DIR)/package.mk

define Package/libogg
	CATEGORY:=Libraries
	TITLE:=libogg
	URL:=http://mad.sourceforge.net
	DEPENDS:=+zlib
endef

define Package/libogg/description
	libogg
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

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ogg $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libogg.{a,so,so.0,so.0.8.2} $(1)/usr/lib
endef

define Package/libogg/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libogg.{a,so,so.0,so.0.8.2} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libogg))
