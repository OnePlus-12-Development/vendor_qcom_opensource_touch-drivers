
KDIR := $(TOP)/kernel_platform/common

ifeq ($(CONFIG_ARCH_WAIPIO), y)
	include $(TOUCH_ROOT)/config/gki_waipiotouch.conf
	LINUX_INC += -include $(TOUCH_ROOT)/config/gki_waipiotouchconf.h
endif

LINUX_INC +=	-Iinclude/linux \
		-Iinclude/linux/drm \
		-Iinclude/linux/gunyah \
		-Iinclude/linux/input

CDEFINES +=	-DANI_LITTLE_BYTE_ENDIAN \
	-DANI_LITTLE_BIT_ENDIAN \
	-DDOT11F_LITTLE_ENDIAN_HOST \
	-DANI_COMPILER_TYPE_GCC \
	-DANI_OS_TYPE_ANDROID=6 \
	-DPTT_SOCK_SVC_ENABLE \
	-Wall\
	-Werror\
	-D__linux__

KBUILD_CPPFLAGS += $(CDEFINES)

ccflags-y += $(LINUX_INC)

ifeq ($(call cc-option-yn, -Wmaybe-uninitialized),y)
EXTRA_CFLAGS += -Wmaybe-uninitialized
endif

ifeq ($(call cc-option-yn, -Wheader-guard),y)
EXTRA_CFLAGS += -Wheader-guard
endif

######### CONFIG_MSM_TOUCH ########

ifeq ($(CONFIG_TOUCHSCREEN_SYNAPTICS_DSX), y)

	LINUX_INC += -include $(TOUCH_ROOT)/synaptics_dsx/synaptics_dsx.h
	LINUX_INC += -include $(TOUCH_ROOT)/synaptics_dsx/synaptics_dsx_core.h

	synaptics_dsx-y := \
		 ./synaptics_dsx/synaptics_dsx_core.o \
		 ./synaptics_dsx/synaptics_dsx_i2c.o

	obj-$(CONFIG_MSM_TOUCH) += synaptics_dsx.o
endif

ifeq ($(CONFIG_TOUCH_FOCALTECH), y)
	LINUX_INC += -include $(TOUCH_ROOT)/focaltech_touch/focaltech_common.h
	LINUX_INC += -include $(TOUCH_ROOT)/focaltech_touch/focaltech_config.h
	LINUX_INC += -include $(TOUCH_ROOT)/focaltech_touch/focaltech_core.h
	LINUX_INC += -include $(TOUCH_ROOT)/focaltech_touch/focaltech_flash.h

	focaltech_fts-y := \
		 ./focaltech_touch/focaltech_core.o \
		 ./focaltech_touch/focaltech_ex_fun.o \
		 ./focaltech_touch/focaltech_ex_mode.o \
		 ./focaltech_touch/focaltech_gesture.o \
		 ./focaltech_touch/focaltech_esdcheck.o \
		 ./focaltech_touch/focaltech_point_report_check.o \
		 ./focaltech_touch/focaltech_i2c.o \
		 ./focaltech_touch/focaltech_flash.o \
		 ./focaltech_touch/focaltech_flash/focaltech_upgrade_ft3518.o

	obj-$(CONFIG_MSM_TOUCH) += focaltech_fts.o
endif

ifeq ($(CONFIG_TOUCHSCREEN_NT36XXX_I2C), y)
	LINUX_INC += -include $(TOUCH_ROOT)/nt36xxx/nt36xxx.h
	LINUX_INC += -include $(TOUCH_ROOT)/nt36xxx/nt36xxx_mem_map.h
	LINUX_INC += -include $(TOUCH_ROOT)/nt36xxx/nt36xxx_mp_ctrlram.h

	nt36xxx-i2c-y := \
		 ./nt36xxx/nt36xxx.o \
		 ./nt36xxx/nt36xxx_fw_update.o \
		 ./nt36xxx/nt36xxx_ext_proc.o \
		 ./nt36xxx/nt36xxx_mp_ctrlram.o

	obj-$(CONFIG_MSM_TOUCH) += nt36xxx-i2c.o
endif

CDEFINES += -DBUILD_TIMESTAMP=\"$(shell date -u +'%Y-%m-%dT%H:%M:%SZ')\"
