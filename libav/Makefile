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
	$(call Build/Compile/Default, -f Makefile)
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
		--disable-vhook
endef

LIBAVUTIL_HEADERS= $(PKG_BUILD_DIR)/libavutil/adler32.h \
          $(PKG_BUILD_DIR)/libavutil/avstring.h \
          $(PKG_BUILD_DIR)/libavutil/avutil.h \
          $(PKG_BUILD_DIR)/libavutil/base64.h \
          $(PKG_BUILD_DIR)/libavutil/common.h \
          $(PKG_BUILD_DIR)/libavutil/crc.h \
          $(PKG_BUILD_DIR)/libavutil/fifo.h \
          $(PKG_BUILD_DIR)/libavutil/intfloat_readwrite.h \
          $(PKG_BUILD_DIR)/libavutil/log.h \
          $(PKG_BUILD_DIR)/libavutil/lzo.h \
          $(PKG_BUILD_DIR)/libavutil/mathematics.h \
          $(PKG_BUILD_DIR)/libavutil/md5.h \
          $(PKG_BUILD_DIR)/libavutil/mem.h \
          $(PKG_BUILD_DIR)/libavutil/pixfmt.h \
          $(PKG_BUILD_DIR)/libavutil/random.h \
          $(PKG_BUILD_DIR)/libavutil/rational.h \
          $(PKG_BUILD_DIR)/libavutil/sha1.h

LIBAVFORMAT_HEADERS = $(PKG_BUILD_DIR)/libavformat/avformat.h \
					  $(PKG_BUILD_DIR)/libavformat/avio.h

LIBAVCODEC_HEADERS = $(PKG_BUILD_DIR)/libavcodec/avcodec.h \
					 $(PKG_BUILD_DIR)/libavcodec/opt.h \
					 $(PKG_BUILD_DIR)/libavcodec/vdpau.h \
					 $(PKG_BUILD_DIR)/libavcodec/xvmc.h

define Package/libav/install
	$(INSTALL_DIR) $(1)/usr/lib

	$(INSTALL_DIR) $(1)/usr/include/libavutil
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavutil/libavutil.so $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavutil/libavutil.so.* $(1)/usr/lib
	$(INSTALL_DATA) $(LIBAVUTIL_HEADERS) $(1)/usr/include/libavutil

	$(INSTALL_DIR) $(1)/usr/include/libavformat	
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavformat/libavformat.so $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavformat/libavformat.so.* $(1)/usr/lib
	$(INSTALL_DATA) $(LIBAVFORMAT_HEADERS) $(1)/usr/include/libavformat

	$(INSTALL_DIR) $(1)/usr/include/libavcodec
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavcodec/libavcodec.so $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libavcodec/libavcodec.so.* $(1)/usr/lib
	$(INSTALL_DATA) $(LIBAVCODEC_HEADERS) $(1)/usr/include/libavcodec
endef

$(eval $(call BuildPackage,libav))
