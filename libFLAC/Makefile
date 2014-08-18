include $(TOPDIR)/rules.mk

PKG_NAME:=libFLAC
PKG_VERSION:=1.3.0
PKG_RELEASE:=1.3.0

PKG_BUILD_DIR=$(BUILD_DIR)/flac-$(PKG_VERSION)
PKG_SOURCE:=flac-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://downloads.xiph.org/releases/flac
PKG_MD5SUM:=13b5c214cee8373464d3d65dee362cdd

include $(INCLUDE_DIR)/package.mk

define Package/libFLAC
	CATEGORY:=Libraries
	TITLE:=libFLAC
	URL:=http://mad.sourceforge.net
	DEPENDS:=+libiconv +libogg
endef

define Package/libFLAC/description
	libFLAC
endef

TARGET_CFLAGS += -fPIC 
TARGET_CXXFLAGS += -fPIC
define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

TARGET_LDFLAGS += -logg -liconv
define Build/Configure
	cd $(PKG_BUILD_DIR) && \
		CC="$(TARGET_CC)" LDLAGS="$(TARGET_LDFLAGS)" \
		./configure \
		--prefix=/usr \
		--with-ogg="$(STAGING_DIR)/usr" \
		--with-libiconv-prefix="$(STAGING_DIR)/usr" \
		--host=$(ARCH)-linux \
	    --disable-thorough-tests \
		--disable-oggtest \
		--disable-doxygen-docs
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/FLAC $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/FLAC++ $(1)/usr/include

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libFLAC.{a,so,so.8,so.8.3.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libFLAC++.{a,so,so.6,so.6.3.0} $(1)/usr/lib
endef

define Package/libFLAC/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libFLAC.{a,so,so.8,so.8.3.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libFLAC++.{a,so,so.6,so.6.3.0} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libFLAC))
