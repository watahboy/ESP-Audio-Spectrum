GZIP_COMPRESSION ?= no
USE_HEATSHRINK ?= yes

TARGET = mkespfsimage.exe

CC = gcc
LD = $(CC)
CFLAGS=-c -I../../lib/heatshrink -I.. -Imman-win32 -std=gnu99
LDFLAGS=-Lmman-win32 -lmman 

ifeq ("$(GZIP_COMPRESSION)","yes")
CFLAGS += -DESPFS_GZIP
LDFLAGS += -lz
endif

ifeq ("$(USE_HEATSHRINK)","yes")
CFLAGS += -DESPFS_HEATSHRINK
endif

OBJECTS = main.o heatshrink_encoder.o

all: libmman $(TARGET)

libmman:
	$(Q) make -C mman-win32

$(TARGET): $(OBJECTS)
	$(LD) -o $@ $^ $(LDFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) -o $@ $^

clean:
	rm -f $(OBJECTS) $(TARGET)

.PHONY: all clean
