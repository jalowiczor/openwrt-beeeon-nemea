#
# Copyright (c) 2016, 2017, Brno University of Technology
#
# This is free software, licensed under the BSD-3-Clause.
#
# This file is based on
# https://github.com/BeeeOn/openwrt-packages/tree/master/beeeon-gateway
#

include $(TOPDIR)/rules.mk

PKG_NAME:=beeeon-gateway-with-nemea
PKG_VERSION:=v2018.07.1
PKG_RELEASE:=rc4
INIT_SCRIPT_NAME:=$(PKG_NAME)

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=+libmosquittopp +poco +zmq +cppzmq +openzwave +cppunit +bluez-libs +libpcap +nemea-framework
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

# Source settings (i.e. where to find the source codes)
# This is a custom variable, used below
SOURCE_DIR:=src

CMAKE_OPTIONS += \
	-DCMAKE_INSTALL_PREFIX=/ \
	-DCMAKE_BUILD_TYPE:STRING=Release \
	-DENABLE_UCLIBCXX_FIXES=OFF \
	-DENABLE_UDEV=OFF \
	-DENABLE_FITP=OFF \
	-DENABLE_TESTS=OFF

TARGET_CFLAGS += -DPOCO_NO_FPENVIRONMENT

define Package/$(PKG_NAME)
	TITLE:=Main application for BeeeOn Gateway
	DEPENDS:=+poco +libmosquittopp +libzmq-nc +cppunit +openzwave +bluez-libs +libpcap +nemea-framework
	MAINTAINER:=Jakub Jalowiczor <jakub.jalowiczor@vsb.cz>
endef

define Package/$(PKG_NAME)/description
 Main application for BeeeOn Gateway.
endef

# Package preparation instructions; create the build directory and copy the source code.
# The last command is necessary to ensure our preparation instructions remain compatible with the patching system.
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -r $(SOURCE_DIR)/* $(PKG_BUILD_DIR)
	$(Build/Patch)
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
