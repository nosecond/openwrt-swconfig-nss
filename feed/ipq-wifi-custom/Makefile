include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/version.mk

PKG_NAME:=ipq-wifi-custom
PKG_RELEASE:=1
PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Build/Compile
endef

define Build/Prepare
	$(call Build/Prepare/Default,)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

ALLWIFIBOARDS:= \
	honor_xd27

ALLWIFIPACKAGES:=$(foreach BOARD,$(ALLWIFIBOARDS),ipq-wifi-$(BOARD))

define Package/ipq-wifi-default
  SUBMENU:=ath11k Board-Specific Overrides
  SECTION:=firmware
  CATEGORY:=Firmware
  DEPENDS:=@TARGET_qualcommax_ipq50xx
  TITLE:=Custom Board
endef

define ipq-wifi-install-ath11-one-to
  $(INSTALL_DIR)  $(2)/lib/firmware/ath11k/$(3)/
  $(INSTALL_DATA) $(1) $(2)/lib/firmware/ath11k/$(3)/board-2.bin
endef

define ipq-wifi-install-one
  $(if $(filter $(suffix $(1)),.IPQ5018 .ipq5018),\
    $(call ipq-wifi-install-ath11-one-to,$(1),$(2),IPQ5018/hw1.0),\
  $(if $(filter $(suffix $(1)),.QCN6122 .qcn6122),\
    $(call ipq-wifi-install-ath11-one-to,$(1),$(2),QCN6122/hw1.0),\
  $(if $(filter $(suffix $(1)),.QCN9074 .qcn9074),\
    $(call ipq-wifi-install-ath11-one-to,$(1),$(2),QCN9074/hw1.0),\
    $(error Unrecognized board-file suffix '$(suffix $(1))' for '$(1)')\
  )))

endef

define generate-ipq-wifi-package
  define Package/ipq-wifi-$(1)
    $(call Package/ipq-wifi-default)
    TITLE:=board-2.bin Overrides for $(2)
    CONFLICTS:=$(PREV_BOARD)
  endef

  define Package/ipq-wifi-$(1)/description
    Device specific ath11k board data
  endef

  define Package/ipq-wifi-$(1)/install-overlay
    $$$$(foreach IPQ_WIFI_BOARD_FILE,$$$$(wildcard $(PKG_BUILD_DIR)/board-$(1).*),\
      $$$$(call ipq-wifi-install-one,$$$$(IPQ_WIFI_BOARD_FILE),$$(1)))
  endef

  PREV_BOARD+=ipq-wifi-$(1)
endef

$(eval $(call generate-ipq-wifi-package,honor_xd27,HONOR XD27))

$(foreach PACKAGE,$(ALLWIFIPACKAGES),$(eval $(call BuildPackage,$(PACKAGE))))

