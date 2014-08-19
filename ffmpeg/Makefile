include $(TOPDIR)/rules.mk

PKG_NAME:=ffmpeg
PKG_VERSION:=2.3.3
PKG_RELEASE:=2

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://ffmpeg.org/releases
PKG_MD5SUM:=72361d3b8717b6db3ad2b9da8df7af5e

include $(INCLUDE_DIR)/package.mk

define Package/ffmpeg
	SECTION:=net
	CATEGORY:=Network
	DEFAULT:=y
	TITLE:=ffmpeg
	URL:=https://ffmpeg.org
	DEPENDS:=+zlib
endef

define Package/ffmpeg/description
	ffmpeg
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

define Package/ffmpeg/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavcodec.{so,so.52,so.52.20.1} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavdevice.{so,so.52,so.52.1.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavformat.{so,so.52,so.52.31.0} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavutil.{so,so.49,so.49.15.0} $(1)/usr/lib
endef

$(eval $(call BuildPackage,ffmpeg))
