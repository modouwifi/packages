include $(TOPDIR)/rules.mk

PKG_NAME:=sqlite3
PKG_VERSION:=27392118af
PKG_RELEASE:=27392118af

PKG_BUILD_DIR=$(BUILD_DIR)/SQLite-$(PKG_VERSION)
PKG_SOURCE:=SQLite-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.sqlite.org/src/tarball
PKG_MD5SUM:=bb43d78e5a951e1498eb073df01c0a8f

include $(INCLUDE_DIR)/package.mk

define Package/sqlite3
	SECTION:=libs
	CATEGORY:=Libraries
	SUBMENU:=Database
	TITLE:=sqlite3
	DEPENDS:=+libcurses +libpthread
	URL:=http://www.sqlite.org
endef

define Package/sqlite3/description
	sqlite3
endef

TARGET_CFLAGS+=-fPIC 
TARGET_CXXFLAGS+=-fPIC
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" all install
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && \
		CC=$(TARGET_CC) CFLAGS="-fPIC" ./configure --prefix=/usr \
		--enable-shared \
		--enable-static \
		--host=mipsel-linux \
		--enable-threadsafe \
		--enable-cross-thread-connections \
		--with-sysroot=$(STAGING_DIR)/lib 
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsqlite3.{a,so,so.0,so.0.8.6} $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/sqlite3.h $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/sqlite3ext.h $(1)/usr/include
endef

define Package/sqlite3/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libsqlite3.{a,so,so.0,so.0.8.6} $(1)/usr/lib
endef

$(eval $(call BuildPackage,sqlite3))
