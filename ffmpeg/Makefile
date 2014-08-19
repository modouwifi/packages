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
	DEPENDS:=+zlib +libpthread
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
		--cross-prefix=mipsel-linux-
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavcodec.{a,so,so.55,so.55.69.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavdevice.{a,so,so.55,so.55.13.102} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavfilter.{a,so,so.4,so.4.11.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavformat.{a,so,so.55,so.55.48.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavutil.{a,so,so.52,so.52.92.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavswresample.{a,so,so.0,so.0.19.100} $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavcodec $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavdevice $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavfilter $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavformat $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libavutil $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libswresample $(1)/usr/include
endef

define Package/ffmpeg/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavcodec.{a,so,so.55,so.55.69.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavdevice.{a,so,so.55,so.55.13.102} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavfilter.{a,so,so.4,so.4.11.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavformat.{a,so,so.55,so.55.48.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavutil.{a,so,so.52,so.52.92.100} $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libavswresample.{a,so,so.0,so.0.19.100} $(1)/usr/lib
endef

$(eval $(call BuildPackage,ffmpeg))
