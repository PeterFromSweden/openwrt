# 
# Copyright (C) 2010 Telldus Technologies AB
#
# This is free software, licensed under the GNU General Public License v2.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/nls.mk

PKG_NAME:=telldus-core
PKG_VERSION:=2.1.2
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://download.telldus.com/TellStick/Software/telldus-core/
PKG_HASH:=a20f6c74814afc23312d2c93ebbb37fdea9deaaee05ae7b6a6275e11e4662014

include $(INCLUDE_DIR)/package.mk

EXTRA_CPPFLAGS:=\
        -I$(ICONV_PREFIX)/include

EXTRA_CFLAGS:=\
        -I$(ICONV_PREFIX)/include

define Package/telldus-core
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Telldus TellStick USB interface
	URL:=http://www.telldus.com
	DEPENDS:=+confuse +libftdi +libstdcpp +argp-standalone +libiconv-full $(ICONV_DEPENDS)
endef
# Note: argp-standalone is needed for compiling (build time only)

define Build/Configure
	cd $(PKG_BUILD_DIR) && \
	$(TARGET_CONFIGURE_OPTS) \
	ICONV_PREFIX=$(ICONV_PREFIX) cmake --debug-output \
		-DBUILD_RFCMD=0 \
		-DCMAKE_LIBRARY_PATH=${STAGING_DIR}/usr/lib \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DBUILD_LIBTELLDUS-CORE=1 \
		-DBUILD_TDTOOL=1 \
		-DSUPPORT_TELLSTICK_DUO=0 \
		-DSUPPORT_USB=0 \
		-DGENERATE_MAN=0 \
		-DUSE_QT_SETTINGS_BACKEND=0

endef

define Package/telldus-core/install
	cd $(PKG_BUILD_DIR) && \
	$(MAKE) DESTDIR=$(1) install
endef

$(eval $(call BuildPackage,telldus-core))
