include $(TOPDIR)/rules.mk

PKG_NAME:=minidlna
PKG_VERSION:=1.1.3
PKG_RELEASE:=1.1

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/minidlna
PKG_MD5SUM:=879027192c89e5376cdd2ae2d1aa33b4

include $(INCLUDE_DIR)/package.mk

define Package/minidlna
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEFAULT:=y
	TITLE:=Minilna
	URL:=http://minidlna.sourceforge.net
	DEPENDS:=+libexif +jpeg +libid3tag \
		     +libFLAC +libvorbis +libogg \
			 +libsqlite3 +ffmpeg
endef

define Package/minidlna/description
	MinidLNA
endef

TARGET_CFLAGS += -fPIC -I$(STAGING_DIR)/usr/include
TARGET_CXXFLAGS += -fPIC -I$(STAGING_DIR)/usr/include

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" all install
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && autoconf && \
		./configure \
		--target=mipsel-linux \
		--host=mipsel-linux \
		--build=x86_64-suse-linux \
		--prefix=/usr \
		--program-prefix="" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		CFLAGS="$(TARGET_CFLAGS)"
endef

define Package/minidlna/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/minidlnad $(1)/usr/sbin
endef

$(eval $(call BuildPackage,minidlna))
