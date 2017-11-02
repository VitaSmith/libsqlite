TARGET_LIB = libsqlite.a
OBJS       = sqlite.o

PREFIX  ?= $(VITASDK)/arm-vita-eabi
CC      = arm-vita-eabi-gcc
AR      = arm-vita-eabi-ar
CFLAGS  = -Wl,-q -Wall -O3
ASFLAGS = $(CFLAGS)

all: $(TARGET_LIB)

debug: CFLAGS += -DDEBUG_BUILD
debug: all

$(TARGET_LIB): $(OBJS)
	$(AR) -rcs $@ $^

clean:
	rm -rf $(TARGET_LIB) $(OBJS)

install: $(TARGET_LIB)
	@mkdir -p $(DESTDIR)$(PREFIX)/lib
	cp $(TARGET_LIB) $(DESTDIR)$(PREFIX)/lib
	@mkdir -p $(DESTDIR)$(PREFIX)/include/psp2
	cp sqlite.h $(DESTDIR)$(PREFIX)/include/psp2
	@echo "Installed!"
