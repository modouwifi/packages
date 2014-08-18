include $(TOPDIR)/rules.mk

PKG_NAME:=libid3tag
PKG_VERSION:=0.15.1b
PKG_RELEASE:=0.15.1b

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/mad/libid3tag
PKG_MD5SUM:=e5808ad997ba32c498803822078748c3

include $(INCLUDE_DIR)/package.mk

define Package/libid3tag
	CATEGORY:=Libraries
	TITLE:=libid3tag
	URL:=http://mad.sourceforge.net
	DEPENDS:=+zlib
endef

define Package/libid3tag/description
	libid3tag
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
	$(CP) $(PKG_INSTALL_DIR)/usr/include/id3tag.h $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libid3tag.{a,so,so.0,so.0.3.0} $(1)/usr/lib
endef

define Package/libid3tag/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libid3tag.{a,so,so.0,so.0.3.0} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libid3tag))
