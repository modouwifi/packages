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
		+libFLAC +libvorbis +libogg +libsqlite3 \
		+libavformat +libavcodec +libavutil
endef

define Package/minidlna/description
	MinidLNA
endef

TARGET_CFLAGS+=-fPIC \
			   -I$(STAGING_DIR)/root-ramips/usr/include
TARGET_CXXFLAGS+=-fPIC \
				 -I$(STAGING_DIR)/root-ramips/usr/include
define Build/Compile
	$(call Build/Compile/Default, -f Makefile CFLAGS="$(TARGET_CFLAGS)")
endef

TARGET_LDFLAGS += -lavformat
define Build/Configure
	$(call Build/Configure/Default, --prefix=/usr \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		CFLAGS="$(TARGET_CFLAGS)")
endef

define Package/minidlna/install
	$(INSTALL_DIR) $(1)/usr/bin
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ $(1)/usr/bin
endef

$(eval $(call BuildPackage,minidlna))
