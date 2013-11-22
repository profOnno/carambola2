#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nss-mdns
PKG_VERSION:=0.10
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://0pointer.de/lennart/projects/nss-mdns/
PKG_MD5SUM:=03938f17646efbb50aa70ba5f99f51d7

PKG_FIXUP:=libtool
PKG_REMOVE_FILES:=autogen.sh

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/nss-mdns
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Incorporate ZEROCONF in host name resolution
  URL:=http://0pointer.de/lennart/projects/nss-mdns/
  MAINTAINER:=Mike Brady <mikebrady@eircom.net>
endef

define Package/nss-mdns/description
 nss-mdns is a plugin for the GNU Name Service Switch (NSS) functionality
 of the GNU C Library (glibc) providing host name resolution via
 Multicast DNS (aka Zeroconf, aka Apple Rendezvous, aka Apple Bonjour),
 effectively allowing name resolution by common Unix/Linux programs
 in the ad-hoc mDNS domain .local.
 
 Relies on avahi to provide the mDNS service.
 Needs OpenWRT to be built using the glibc library.
 Installs the libnss_mdns libraries and suggested settings in
 /etc/nsswitch-README.conf.
 To activate the service, you need to edit /etc/nsswitch.conf -- see
 /etc/nsswitch-README.conf for details and suggested settings.
endef

# Don't ask for documentation to be built.
CONFIGURE_ARGS += \
    --disable-lynx

define Build/Configure
    (cd $(PKG_BUILD_DIR); autoreconf -f)
    $(call Build/Configure/Default, )
endef

define Package/nss-mdns/install
    $(INSTALL_DIR) $(1)/lib
    $(CP) $(PKG_INSTALL_DIR)/usr/lib/libnss_mdns*.so.* $(1)/lib/
        $(INSTALL_DIR) $(1)/etc
    $(INSTALL_DATA) ./files/nsswitch-README.conf $(1)/etc/

endef

$(eval $(call BuildPackage,nss-mdns))
