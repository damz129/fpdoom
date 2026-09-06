NAME = nones
NONES_SRC = src
USE_ASM = 1

APP_SRCS = test scr_update
ifneq ($(USE_ASM), 0)
APP_SRCS += nesasm
endif

NES_SRCS = cpu ppu system cart mapper arena joypad nones utils

APP_OBJS1 = $(APP_SRCS:%=$(OBJDIR)/app/%.o)
APP_OBJS2 = $(NES_SRCS:%=$(OBJDIR)/nes/%.o)

include ../buildinc.make

APP_CFLAGS += -std=c11 -Wall -Wextra -pedantic
APP_CFLAGS += -Wno-strict-prototypes

NES_CFLAGS := $(APP_CFLAGS) -Wno-unused-parameter -Wno-extra-semi
NES_CFLAGS += -DDISABLE_APU -DFP

APP_CFLAGS += -I$(SYSDIR) -I$(NONES_SRC)
ifneq ($(USE_ASM), 0)
APP_CFLAGS += -DUSE_ASM
endif

$(OBJDIR)/nes/%.o: $(NONES_SRC)/%.c | objdir
	$(call compile_cc,$(NES_CFLAGS))

$(OBJDIR)/app/%.o: $(NONES_SRC)/%.c | objdir
	$(call compile_cc,$(APP_CFLAGS))

$(OBJDIR)/app/%.o: $(NONES_SRC)/%.S | objdir
	$(call compile_as,$(APP_CFLAGS))
