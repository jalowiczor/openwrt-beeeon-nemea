#
# Copyright (C) 2017, Brno University of Technology
#
# This is free software, licensed under the BSD-3-Clause.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cppzmq
PKG_VERSION:=4.2.1
PKG_RELEASE:=1
PKG_MAINTAINER:=Tomas Novotny <inovottom@fit.vutbr.cz>
PKG_LICENSE:=MIT

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/zeromq/cppzmq/tar.gz/v$(PKG_VERSION)?
PKG_MD5SUM:=72d1296f26341d136470c25320936683

include $(INCLUDE_DIR)/package.mk

define Package/cppzmq
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=C++ ZeroMQ binding
  URL:=https://github.com/zeromq/cppzmq
endef

define Package/cppzmq/description
 Cppzmq is C++ for 0MQ.
endef

define Build/Compile
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/zmq.hpp $(1)/usr/include
endef

$(eval $(call BuildPackage,cppzmq))
