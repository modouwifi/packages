include $(TOPDIR)/rules.mk

PKG_NAME:=openssh
PKG_VERSION:=6.4p1
PKG_RELEASE:=6

#PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://mirror.jmu.edu/pub/OpenBSD/OpenSSH/portable/
PKG_MD5SUM:=3e9800e6bca1fbac0eea4d41baa7f239

include $(INCLUDE_DIR)/package.mk

define Package/openssh
	SECTION:=net
	CATEGORY:=Network
	DEFAULT:=y
	TITLE:=OpenSSH
	URL:=http://www.openssh.com/
	DEPENDS:=+libopenssl
endef

define Package/openssh/description
	Openssh
endef

TARGET_CFLAGS+=-fPIC
define Build/Compile
	$(call Build/Compile/Default, -f Makefile CFLAGS="$(TARGET_CFLAGS)")
endef

define Build/Configure
	$(call Build/Configure/Default, --prefix=/usr/) 
endef

define Package/openssh/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scp $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sftp $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sftp-server $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-add $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-agent $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sshd $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-keygen $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-keyscan $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-keysign $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssh-pkcs11-helper $(1)/usr/bin/
endef

$(eval $(call BuildPackage,openssh))
