# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mtk-linkit
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/mtk-linkit
	TITLE:=MTK LinkIt Smart board support package
	DEPENDS:=@TARGET_ramips_mt7688_DEVICE_LinkIt7688 \
		+curl +strace +coreutils +coreutils-stty \
		+avahi-nodbus-daemon +mountd \
		+uhttpd +rpcd +rpcd-mod-iwinfo +git +git-http \
		+hidapi +luci +luci-lib-json \
		+rpcd-mod-rpcsys +cgi-io +spi-tools +uboot-envtools \
		+kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core +kmod-i2c-mt7628 \
		+kmod-nls-base +kmod-nls-cp437 +kmod-nls-utf8 \
		+kmod-usb-storage +mtk-linkit-webui +tcpdump-mini
	CATEGORY:=Base system
	DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/mtk-linkit/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/mt7688_pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/mt7688_reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,mtk-linkit))
