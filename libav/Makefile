include $(TOPDIR)/rules.mk

PKG_NAME:=libav
PKG_VERSION:=0.5.10
PKG_RELEASE:=0.5

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://libav.org/releases
PKG_MD5SUM:=a556faf9be2570ad8140dfcea64227df

include $(INCLUDE_DIR)/package.mk

define Package/libav
	SECTION:=net
	CATEGORY:=Network
	DEFAULT:=y
	TITLE:=libav
	URL:=https://libav.org
	DEPENDS:=+zlib
endef

define Package/libav/description
	libav
endef

TARGET_CFLAGS+=-fPIC 
TARGET_CXXFLAGS+=-fPIC
define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" all install
endef

define Build/Configure
	cd $(PKG_BUILD_DIR) && \
	./configure --prefix=/usr \
		--disable-swscale \
		--disable-yasm \
		--enable-shared \
		--arch=mips \
		--enable-cross-compile \
		--target-os=linux \
		--cc="mipsel-linux-cc -fPIC" \
		--disable-ffmpeg \
		--disable-ffplay \
		--disable-ffserver \
		--disable-vhook \
		--cross-prefix=mipsel-linux-
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavcodec.{so,so.52,so.52.20.1} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavdevice.{so,so.52,so.52.1.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavformat.{so,so.52,so.52.31.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavutil.{so,so.49,so.49.15.0} $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavcodec $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavdevice $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavformat $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavutil $(1)/usr/include
endef

define Package/libav/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavcodec.{so,so.52,so.52.20.1} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavdevice.{so,so.52,so.52.1.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavformat.{so,so.52,so.52.31.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavutil.{so,so.49,so.49.15.0} $(1)/usr/lib
endef

$(eval $(call BuildPackage,libav))
