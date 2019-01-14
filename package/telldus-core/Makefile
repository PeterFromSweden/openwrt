# 
# Copyright (C) 2010 Telldus Technologies AB
#
# This is free software, licensed under the GNU General Public License v2.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/nls.mk

PKG_NAME:=telldus-core
PKG_VERSION:=2.1.1
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://download.telldus.com/TellStick/Software/telldus-core/
# PKG_MD5SUM:=adf1994829b5bd1015d8f172b654f309

include $(INCLUDE_DIR)/package.mk

EXTRA_CPPFLAGS:=\
        -I$(ICONV_PREFIX)/include

EXTRA_CFLAGS:=\
        -I$(ICONV_PREFIX)/include

define Package/telldus-core
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Utilities and driver to control NEXA and other RF remote receivers through a TellStick USB interface
	URL:=http://www.telldus.com
	DEPENDS:=+confuse $(ICONV_DEPENDS) libftdi libstdcpp
endef
# Note: argp-standalone is needed for compiling, but is not listed in "DEPENDS";
# there is no package called "argp-standalone" (it is needed at build time only)

#	echo $(ICONV_PREFIX)
#	(env | grep ICONV_)

define Build/Configure
	echo $(ICONV_PREFIX) && \
	cd $(PKG_BUILD_DIR) && \
	$(TARGET_CONFIGURE_OPTS) \
	ICONV_PREFIX=$(ICONV_PREFIX) cmake --debug-output \
		-DBUILD_RFCMD=0 \
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
