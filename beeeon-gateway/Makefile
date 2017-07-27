#
# Copyright (c) 2016, 2017, Brno University of Technology
#
# This is free software, licensed under the BSD-3-Clause.
#
# This file is based on
# https://github.com/BeeeOn/openwrt-packages/tree/master/beeeon-gateway
#

include $(TOPDIR)/rules.mk

PKG_NAME:=beeeon-gateway
PKG_VERSION:=1.0
PKG_RELEASE:=2
INIT_SCRIPT_NAME:=$(PKG_NAME)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_PROTO:=git
PKG_BUILD_DEPENDS:=+libmosquittopp +poco +zmq +cppzmq +openzwave +cppunit
PKG_SOURCE_URL:=https://github.com/BeeeOn/gateway-frc.git
PKG_SOURCE_VERSION:=b5bcebd6dc068394906e35d989ed48dc65e9ebaf

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += \
	-DCMAKE_INSTALL_PREFIX=/ \
	-DCMAKE_BUILD_TYPE:STRING=Release

TARGET_CXXFLAGS += -DPOCO_NO_FPENVIRONMENT

define Package/$(PKG_NAME)
	TITLE:=$(PKG_NAME)
	DEPENDS:=+poco +libmosquittopp +libzmq-nc +cppunit +openzwave
	MAINTAINER:=Tomas Novotny <inovottom@fit.vutbr.cz>
endef

define Package/$(PKG_NAME)/description
 Main application for BeeeOn Gateway.
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)
	$(CP) -r $(PKG_INSTALL_DIR)/* $(1)

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/$(INIT_SCRIPT_NAME) $(1)/etc/init.d/$(INIT_SCRIPT_NAME)
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
  echo "Enabling and starting $(PKG_NAME) service"
  /etc/init.d/$(INIT_SCRIPT_NAME) enable
  /etc/init.d/$(INIT_SCRIPT_NAME) start
fi
exit 0
endef

define Package/$(PKG_NAME)/prerm
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
  echo "Disabling and stopping $(PKG_NAME) service"
  /etc/init.d/$(INIT_SCRIPT_NAME) disable
  /etc/init.d/$(INIT_SCRIPT_NAME) stop
fi
exit 0
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
