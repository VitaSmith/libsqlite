TITLE_ID = SQLDEM000
TARGET   = sqlite_demo
OBJS     = sqlite_demo.o console.o draw.o font_data.o

LIBS = -lc -lsqlite -lSceSqlite_stub -lSceDisplay_stub \
	-lSceGxm_stub -lSceCtrl_stub -lSceAppUtil_stub \
	-lSceSysmodule_stub

PREFIX  = arm-vita-eabi
CC      = $(PREFIX)-gcc
CFLAGS  = -Wl,-q -Wall -O3
ASFLAGS = $(CFLAGS)

all: $(TARGET).vpk

debug: CFLAGS += -DSHOW_DEBUG=1
debug: all

%.vpk: eboot.bin
	vita-mksfoex -s TITLE_ID=$(TITLE_ID) "$(TARGET)" param.sfo
	vita-pack-vpk -s param.sfo -b eboot.bin $@

eboot.bin: $(TARGET).velf
	vita-make-fself -s $< $@

%.velf: %.elf
	vita-elf-create $< $@

$(TARGET).elf: $(OBJS)
	$(CC) $(CFLAGS) $^ $(LIBS) -o $@

install: eboot.bin
	@cp -v eboot.bin /g/app/$(TITLE_ID)/

clean:
	@rm -rf $(TARGET).vpk $(TARGET).velf $(TARGET).elf $(OBJS) \
		eboot.bin param.sfo
