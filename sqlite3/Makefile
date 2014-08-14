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
	$(call Build/Compile/Default, -f Makefile)
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

HEADERS= $(PKG_BUILD_DIR)/sqlite3.h \
		 $(PKG_BUILD_DIR)/sqlite3ext.h

define Package/sqlite3/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/libsqlite3.so.0.8.6 $(1)/usr/lib/libsqlite3.so.0.8.6
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/.libs/libsqlite3.so $(1)/usr/lib/libsqlite3.so
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/.libs/libsqlite3.so.0 $(1)/usr/lib/libsqlite3.so.0
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/libsqlite3.a $(1)/usr/lib/libsqlite3.a
	$(TARGET_RANLIB) $(1)/usr/lib/libsqlite3.a

	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DATA) $(HEADERS) $(1)/usr/include
endef

$(eval $(call BuildPackage,sqlite3))
