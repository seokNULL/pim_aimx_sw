CC ?= gcc

CFLAGS += -g
#CFLAGS += -O2 -fno-inline -Wall -Wstrict-prototypes
CFLAGS += -I. -I../include -I../dma-utils
CFLAGS += $(EXTRA_FLAGS)
# LIBS=-lpim

DMA-XFER = mem-cpy
DMA-UTILS_OBJS := $(patsubst %.c,%.o,$(wildcard ../dma-utils/*.c))
# DMA-XFER_OBJS := main.o dmaxfer.o
DMA-XFER_OBJS := main.o
DMA-XFER_OBJS += $(DMA-UTILS_OBJS)

ifneq ($(CROSS_COMPILE_FLAG),)
	CC=$(CROSS_COMPILE_FLAG)gcc
endif

all: clean mem-cpy

mem-cpy: $(DMA-XFER_OBJS)
	$(CC) -pthread -lrt  $^ -o $(DMA-XFER) -laio -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -D_LARGE_FILE_SOURCE -lpim -lpthread

%.o: %.c
	$(CC) $(CFLAGS) -c -std=c99 -o $@ $< -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -D_LARGE_FILE_SOURCE -D_AIO_AIX_SOURCE

clean:
	@rm -f *.o */*.o ../dma-utils/*.o
	rm -rf *.o *.bin dma-xfer
