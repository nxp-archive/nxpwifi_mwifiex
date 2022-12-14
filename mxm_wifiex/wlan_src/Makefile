#  File: Makefile
#
#  Copyright 2014-2020 NXP
#
#  This software file (the File) is distributed by NXP
#  under the terms of the GNU General Public License Version 2, June 1991
#  (the License).  You may use, redistribute and/or modify the File in
#  accordance with the terms and conditions of the License, a copy of which
#  is available by writing to the Free Software Foundation, Inc.,
#  51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA or on the
#  worldwide web at http://www.gnu.org/licenses/old-licenses/gpl-2.0.txt.
#
#  THE FILE IS DISTRIBUTED AS-IS, WITHOUT WARRANTY OF ANY KIND, AND THE
#  IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE
#  ARE EXPRESSLY DISCLAIMED.  The License provides additional details about
#  this warranty disclaimer.
#

COMPATDIR=/lib/modules/$(KERNELVERSION_X86)/build/compat-wireless-3.2-rc1-1/include
ifeq ($(CC),)
CC ?=		$(CROSS_COMPILE)gcc -I$(COMPATDIR)
endif
ifeq ($(LD),)
LD=		$(CROSS_COMPILE)ld
endif
BACKUP=		/root/backup
YMD=		`date +%Y%m%d%H%M`

#############################################################################
# Configuration Options
#############################################################################
# Multi-chipsets
CONFIG_SD8887=n
CONFIG_SD8897=n
CONFIG_USB8897=n
CONFIG_PCIE8897=n
CONFIG_SD8977=n
CONFIG_SD8978=n
CONFIG_USB8978=n
CONFIG_SD8997=n
CONFIG_USB8997=n
CONFIG_PCIE8997=y
CONFIG_SD8987=y
CONFIG_SD9097=n
CONFIG_USB9097=n
CONFIG_PCIE9097=n
CONFIG_SD9098=n
CONFIG_USB9098=n
CONFIG_PCIE9098=n


# Debug Option
# DEBUG LEVEL n/1/2:
# n: NO DEBUG
# 1: Only PRINTM(MMSG,...), PRINTM(MFATAL,...), ...
# 2: All PRINTM()
CONFIG_DEBUG=1

# Enable STA mode support
CONFIG_STA_SUPPORT=y

# Enable uAP mode support
CONFIG_UAP_SUPPORT=y

# Enable WIFIDIRECT support
CONFIG_WIFI_DIRECT_SUPPORT=y


# Re-association in driver
CONFIG_REASSOCIATION=y


# Manufacturing firmware support
CONFIG_MFG_CMD_SUPPORT=y

# OpenWrt support
CONFIG_OPENWRT_SUPPORT=n

# Big-endian platform
CONFIG_BIG_ENDIAN=n



ifeq ($(CONFIG_DRV_EMBEDDED_SUPPLICANT), y)
CONFIG_EMBEDDED_SUPP_AUTH=y
else
ifeq ($(CONFIG_DRV_EMBEDDED_AUTHENTICATOR), y)
CONFIG_EMBEDDED_SUPP_AUTH=y
endif
endif

#ifdef SDIO_MMC
# SDIO suspend/resume
CONFIG_SDIO_SUSPEND_RESUME=y
#endif

# DFS testing support
CONFIG_DFS_TESTING_SUPPORT=y




# Use static link for app build
CONFIG_ANDROID_KERNEL=n

#32bit app over 64bit kernel support
CONFIG_USERSPACE_32BIT_OVER_KERNEL_64BIT=n


#############################################################################
# Select Platform Tools
#############################################################################

ccflags-y += -DLINUX

KERNELVERSION_X86 :=   $(shell uname -r)
KERNELDIR ?= /lib/modules/$(KERNELVERSION_X86)/build
LD += -S

BINDIR = ../bin_mxm_wifiex
APPDIR= $(shell if test -d "mapp"; then echo mapp; fi)

#############################################################################
# Compiler Flags
#############################################################################

	ccflags-y += -I$(KERNELDIR)/include

	ccflags-y += -DFPNUM='"92"'

ifeq ($(CONFIG_DEBUG),1)
	ccflags-y += -DDEBUG_LEVEL1
endif

ifeq ($(CONFIG_DEBUG),2)
	ccflags-y += -DDEBUG_LEVEL1
	ccflags-y += -DDEBUG_LEVEL2
	DBG=	-dbg
endif

ifeq ($(CONFIG_64BIT), y)
	ccflags-y += -DMLAN_64BIT
endif

ifeq ($(CONFIG_STA_SUPPORT),y)
	ccflags-y += -DSTA_SUPPORT
ifeq ($(CONFIG_REASSOCIATION),y)
	ccflags-y += -DREASSOCIATION
endif
else
CONFIG_WIFI_DIRECT_SUPPORT=n
CONFIG_STA_WEXT=n
CONFIG_STA_CFG80211=n
endif

ifeq ($(CONFIG_UAP_SUPPORT),y)
	ccflags-y += -DUAP_SUPPORT
else
CONFIG_WIFI_DIRECT_SUPPORT=n
CONFIG_UAP_WEXT=n
CONFIG_UAP_CFG80211=n
endif

ifeq ($(CONFIG_WIFI_DIRECT_SUPPORT),y)
	ccflags-y += -DWIFI_DIRECT_SUPPORT
endif

ifeq ($(CONFIG_MFG_CMD_SUPPORT),y)
	ccflags-y += -DMFG_CMD_SUPPORT
endif

ifeq ($(CONFIG_BIG_ENDIAN),y)
	ccflags-y += -DBIG_ENDIAN_SUPPORT
endif

ifeq ($(CONFIG_USERSPACE_32BIT_OVER_KERNEL_64BIT),y)
	ccflags-y += -DUSERSPACE_32BIT_OVER_KERNEL_64BIT
endif

#ifdef SDIO_MMC
ifeq ($(CONFIG_SDIO_SUSPEND_RESUME),y)
	ccflags-y += -DSDIO_SUSPEND_RESUME
endif
#endif


ifeq ($(CONFIG_DFS_TESTING_SUPPORT),y)
	ccflags-y += -DDFS_TESTING_SUPPORT
endif


ifeq ($(CONFIG_ANDROID_KERNEL), y)
	ccflags-y += -DANDROID_KERNEL
endif

ifeq ($(CONFIG_OPENWRT_SUPPORT), y)
	ccflags-y += -DOPENWRT
endif

ifeq ($(CONFIG_T50), y)
	ccflags-y += -DT50
	ccflags-y += -DT40
	ccflags-y += -DT3T
endif

ifeq ($(CONFIG_SD8887),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8887
endif
ifeq ($(CONFIG_SD8897),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8897
endif
ifeq ($(CONFIG_SD8977),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8977
endif
ifeq ($(CONFIG_SD8978),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8978
endif
ifeq ($(CONFIG_SD8997),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8997
endif
ifeq ($(CONFIG_SD8987),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD8987
endif
ifeq ($(CONFIG_SD9097),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD9097
endif
ifeq ($(CONFIG_SD9098),y)
	CONFIG_SDIO=y
	ccflags-y += -DSD9098
endif
ifeq ($(CONFIG_USB8897),y)
	CONFIG_MUSB=y
	ccflags-y += -DUSB8897
endif
ifeq ($(CONFIG_USB8997),y)
	CONFIG_MUSB=y
	ccflags-y += -DUSB8997
endif
ifeq ($(CONFIG_USB8978),y)
	CONFIG_MUSB=y
	ccflags-y += -DUSB8978
endif
ifeq ($(CONFIG_USB9097),y)
	CONFIG_MUSB=y
	ccflags-y += -DUSB9097
endif
ifeq ($(CONFIG_USB9098),y)
	CONFIG_MUSB=y
	ccflags-y += -DUSB9098
endif
ifeq ($(CONFIG_PCIE8897),y)
	CONFIG_PCIE=y
	ccflags-y += -DPCIE8897
endif
ifeq ($(CONFIG_PCIE8997),y)
	CONFIG_PCIE=y
	ccflags-y += -DPCIE8997
endif
ifeq ($(CONFIG_PCIE9097),y)
	CONFIG_PCIE=y
	ccflags-y += -DPCIE9097
endif
ifeq ($(CONFIG_PCIE9098),y)
	CONFIG_PCIE=y
	ccflags-y += -DPCIE9098
endif
ifeq ($(CONFIG_SDIO),y)
	ccflags-y += -DSDIO
	ccflags-y += -DSDIO_MMC
endif
ifeq ($(CONFIG_MUSB),y)
	ccflags-y += -DUSB
endif
ifeq ($(CONFIG_PCIE),y)
	ccflags-y += -DPCIE
endif

ifeq ($(CONFIG_MAC80211_SUPPORT),y)
	ccflags-y += -DMAC80211_SUPPORT
endif
ifeq ($(CONFIG_MAC80211_SUPPORT_UAP),y)
	ccflags-y += -DMAC80211_SUPPORT_UAP
endif
ifeq ($(CONFIG_MAC80211_SUPPORT_MESH),y)
	ccflags-y += -DMAC80211_SUPPORT_MESH
endif

# add -Wno-packed-bitfield-compat when GCC version greater than 4.4
GCC_VERSION := $(shell echo `gcc -dumpversion | cut -f1-2 -d.` \>= 4.4 | sed -e 's/\./*100+/g' | bc )
ifeq ($(GCC_VERSION),1)
	ccflags-y += -Wno-packed-bitfield-compat
endif
WimpGCC_VERSION := $(shell echo `gcc -dumpversion | cut -f1 -d.`| bc )
ifeq ($(shell test $(WimpGCC_VERSION) -ge 7; echo $$?),0)
ccflags-y += -Wimplicit-fallthrough=3
endif
ccflags-y += -Wno-stringop-overflow
ccflags-y += -Wno-tautological-compare
ccflags-y += -Wno-stringop-truncation

#############################################################################
# Make Targets
#############################################################################

ifneq ($(KERNELRELEASE),)

ifeq ($(CONFIG_WIRELESS_EXT),y)
ifeq ($(CONFIG_WEXT_PRIV),y)
	# Enable WEXT for STA
	CONFIG_STA_WEXT=y
	# Enable WEXT for uAP
	CONFIG_UAP_WEXT=y
else
# Disable WEXT for STA
	CONFIG_STA_WEXT=n
# Disable WEXT for uAP
	CONFIG_UAP_WEXT=n
endif
endif

# Enable CFG80211 for STA
ifeq ($(CONFIG_CFG80211),y)
	CONFIG_STA_CFG80211=y
else
ifeq ($(CONFIG_CFG80211),m)
	CONFIG_STA_CFG80211=y
else
	CONFIG_STA_CFG80211=n
endif
endif

# OpenWrt
ifeq ($(CONFIG_OPENWRT_SUPPORT), y)
ifeq ($(CPTCFG_CFG80211),y)
	CONFIG_STA_CFG80211=y
else
ifeq ($(CPTCFG_CFG80211),m)
	CONFIG_STA_CFG80211=y
else
	CONFIG_STA_CFG80211=n
endif
endif
endif

# Enable CFG80211 for uAP
ifeq ($(CONFIG_CFG80211),y)
	CONFIG_UAP_CFG80211=y
else
ifeq ($(CONFIG_CFG80211),m)
	CONFIG_UAP_CFG80211=y
else
	CONFIG_UAP_CFG80211=n
endif
endif

# OpenWrt
ifeq ($(CONFIG_OPENWRT_SUPPORT), y)
ifeq ($(CPTCFG_CFG80211),y)
	CONFIG_STA_CFG80211=y
else
ifeq ($(CPTCFG_CFG80211),m)
	CONFIG_STA_CFG80211=y
else
	CONFIG_STA_CFG80211=n
endif
endif
endif

ifneq ($(CONFIG_STA_SUPPORT),y)
	CONFIG_WIFI_DIRECT_SUPPORT=n
	CONFIG_STA_WEXT=n
	CONFIG_STA_CFG80211=n
endif

ifneq ($(CONFIG_UAP_SUPPORT),y)
	CONFIG_WIFI_DIRECT_SUPPORT=n
	CONFIG_UAP_WEXT=n
	CONFIG_UAP_CFG80211=n
endif

ifeq ($(CONFIG_STA_SUPPORT),y)
ifeq ($(CONFIG_STA_WEXT),y)
	ccflags-y += -DSTA_WEXT
endif
ifeq ($(CONFIG_STA_CFG80211),y)
	ccflags-y += -DSTA_CFG80211
endif
endif
ifeq ($(CONFIG_UAP_SUPPORT),y)
ifeq ($(CONFIG_UAP_WEXT),y)
	ccflags-y += -DUAP_WEXT
endif
ifeq ($(CONFIG_UAP_CFG80211),y)
	ccflags-y += -DUAP_CFG80211
endif
endif

print:
ifeq ($(CONFIG_STA_SUPPORT),y)
ifeq ($(CONFIG_STA_WEXT),n)
ifeq ($(CONFIG_STA_CFG80211),n)
	@echo "Can not build STA without WEXT or CFG80211"
	exit 2
endif
endif
endif
ifeq ($(CONFIG_UAP_SUPPORT),y)
ifeq ($(CONFIG_UAP_WEXT),n)
ifeq ($(CONFIG_UAP_CFG80211),n)
	@echo "Can not build UAP without WEXT or CFG80211"
	exit 2
endif
endif
endif

endif

###############################################################

export		CC LD ccflags-y KERNELDIR

.PHONY: mapp/mlanconfig mapp/mlanutl clean distclean
	@echo "Finished Making NXP Wlan Linux Driver"

mapp/mlanconfig:
	$(MAKE) -C $@
mapp/mlanutl:
	$(MAKE) -C $@

echo:

build:

	@if [ ! -d $(BINDIR) ]; then \
		mkdir $(BINDIR); \
	fi

	cp -rpf script/load $(BINDIR)/
	cp -rpf script/unload $(BINDIR)/

	cp -f README_MLAN $(BINDIR)
ifneq ($(APPDIR),)
	$(MAKE) -C mapp/mlanconfig $@ INSTALLDIR=$(BINDIR)
	$(MAKE) -C mapp/mlanutl $@ INSTALLDIR=$(BINDIR)
endif

clean:
	-find . -name "*.o" -exec rm {} \;
	-find . -name "*.ko" -exec rm {} \;
	-find . -name ".*.cmd" -exec rm {} \;
	-find . -name "*.mod.c" -exec rm {} \;
	-find . -name "*.mod" -exec rm {} \;
	-find . -name "Module.symvers" -exec rm {} \;
	-find . -name "Module.markers" -exec rm {} \;
	-find . -name "modules.order" -exec rm {} \;
	-find . -name ".*.dwo" -exec rm {} \;
	-find . -name "*dwo" -exec rm {} \;
	-rm -rf .tmp_versions
ifneq ($(APPDIR),)
	$(MAKE) -C mapp/mlanconfig $@
	$(MAKE) -C mapp/mlanutl $@
endif
#ifdef SDIO
#endif // SDIO

install: default

	echo $(INSTALLDIR)
	echo "MX Driver Installed"

distclean:
	-find . -name "*.o" -exec rm {} \;
	-find . -name "*.orig" -exec rm {} \;
	-find . -name "*.swp" -exec rm {} \;
	-find . -name "*.*~" -exec rm {} \;
	-find . -name "*~" -exec rm {} \;
	-find . -name "*.d" -exec rm {} \;
	-find . -name "*.a" -exec rm {} \;
	-find . -name "tags" -exec rm {} \;
	-find . -name ".*" -exec rm -rf 2> /dev/null \;
	-find . -name "*.ko" -exec rm {} \;
	-find . -name ".*.cmd" -exec rm {} \;
	-find . -name "*.mod.c" -exec rm {} \;
	-find . -name ".*.dwo" -exec rm {} \;
	-find . -name "*dwo" -exec rm {} \;
	-rm -rf .tmp_versions
ifneq ($(APPDIR),)
	$(MAKE) -C mapp/mlanconfig $@
	$(MAKE) -C mapp/mlanutl $@
endif

# End of file
