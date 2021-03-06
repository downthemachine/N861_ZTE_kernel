DHDCFLAGS = -Wall -Wstrict-prototypes \
	-DBCMDRIVER -DBCMSDIO -DBCMLXSDMMC -DBCMPLATFORM_BUS -DBDC -DTOE \
	-DDHDTHREAD -DWIFI_ACT_FRAME  \
	-DGET_CUSTOM_MAC_ENABLE \
	-Idrivers/net/wireless/bcmdhd -Idrivers/net/wireless/bcmdhd/include

# Android specific definition
DHDCFLAGS += -DOEM_ANDROID 
# Pre-init chip when driver starting.
DHDCFLAGS += -DEMBEDDED_PLATFORM
# Platform driver enabled for GPIO control, card detect and getting information of Wi-Fi chip
DHDCFLAGS += -DCUSTOMER_HW2 -DCONFIG_WIFI_CONTROL_FUNC
# Support the sdio_reset_comm(). Quick back to live when system resuming.
DHDCFLAGS += -DMMC_SDIO_ABORT
# Use HW_OOB as default. HW_OOB is level-trigger
DHDCFLAGS += -DHW_OOB -DOOB_INTR_ONLY -DCUSTOM_OOB_GPIO_NUM=0
# Send out the null packet in period to keep the connection with AP
DHDCFLAGS += -DKEEP_ALIVE
# Debug flags
DHDCFLAGS += -DBCMDBG -DSDTEST -DSHOW_EVENTS
# For ICS build-in mode without module removing anymore
DHDCFLAGS += -DENABLE_INSMOD_NO_FW_LOAD 

DHDCFLAGS += -DARP_OFFLOAD_SUPPORT
DHDCFLAGS += -DPKT_FILTER_SUPPORT
DHDCFLAGS += -DPNO_SUPPORT
DHDCFLAGS += -DWMM_PS

DHDOFILES = aiutils.o bcmsdh_sdmmc_linux.o dhd_linux.o siutils.o bcmutils.o   \
	dhd_linux_sched.o bcmwifi.o dhd_sdio.o bcmevent.o hndpmu.o  \
	bcmsdh.o dhd_cdc.o bcmsdh_linux.o dhd_common.o linux_osl.o            \
	bcmsdh_sdmmc.o dhd_custom_gpio.o sbutils.o wldev_common.o wl_android.o

obj-$(CONFIG_BCMDHD) += bcmdhd.o
bcmdhd-objs += $(DHDOFILES)
ifneq ($(CONFIG_WIRELESS_EXT),)
bcmdhd-objs += wl_iw.o
DHDCFLAGS += -DSOFTAP -DCSCAN
endif
ifneq ($(CONFIG_CFG80211),)
bcmdhd-objs += wl_cfg80211.o dhd_cfg80211.o wl_cfgp2p.o wl_linux_mon.o
DHDCFLAGS += -DWL_CFG80211
# P2P support
DHDCFLAGS += -DWLP2P
# WAPI support
DHDCFLAGS += -DBCMWAPI_WPI -DBCMWAPI_WAI
endif
EXTRA_CFLAGS = $(DHDCFLAGS)
ifeq ($(CONFIG_BCMDHD),m)
DHDCFLAGS += -I$(M) -I$(M)/include
EXTRA_LDFLAGS += --strip-debug
endif
