NAME = nones

USE_ASM = 1

APP_SRCS = test scr_update cpu ppu system cart mapper arena joypad nones utils
ifneq ($(USE_ASM), 0)
APP_SRCS += nesasm
endif

APP_OBJS1 = $(APP_SRCS:%=$(OBJDIR)/app/%.o)
APP_OBJS2 = 

include ../buildinc.make

APP_CFLAGS += -std=c11 -Wall -Wextra -pedantic -Wno-strict-prototypes
APP_CFLAGS += -DDISABLE_APU -DFP

APP_CFLAGS += -I$(SYSDIR) -I.
ifneq ($(USE_ASM), 0)
APP_CFLAGS += -DUSE_ASM
endif

$(OBJDIR)/app/%.o: %.c | objdir
	$(call compile_cc,$(APP_CFLAGS))

$(OBJDIR)/app/%.o: %.S | objdir
	$(call compile_as,$(APP_CFLAGS))
