include $(TOPDIR)/rules.mk

PKG_NAME:=libvorbis
PKG_VERSION:=1.3.4
PKG_RELEASE:=1.3.4

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://downloads.xiph.org/releases/vorbis
PKG_MD5SUM:=55f2288055e44754275a17c9a2497391

include $(INCLUDE_DIR)/package.mk

define Package/libvorbis
	CATEGORY:=Libraries
	TITLE:=libvorbis
	URL:=http://mad.sourceforge.net
	DEPENDS:=+zlib
endef

define Package/libvorbis/description
	libvorbis
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
		--with-ogg="$(STAGING_DIR)/usr" \
		--host=mipsel-linux
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/vorbis $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libvorbis.{a,so,so.0,so.0.8.2} $(1)/usr/lib
endef

define Package/libvorbis/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libvorbis.{a,so,so.0,so.0.8.2} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libvorbis))
