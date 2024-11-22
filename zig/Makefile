CC32=zig cc
CC64=$(CC32)
OBJCOPY32=zig objcopy
OBJCOPY64=$(OBJCOPY32)
CFLAGS=-fpic
CPPFLAGS=-O2 -Wall -Wextra -nostdlib

PLATFORM_32_BIT=-target arm-freestanding-eabi
PLATFORM_64_BIT=-target aarch64-freestanding-eabi

CPU_P1=-mcpu=arm1176jzf_s
CPU_P2=-mcpu=cortex_a7
CPU_P3=-mcpu=cortex_a53
CPU_P4=-mcpu=cortex_a72
CPU_P5=-mcpu=cortex_a76

all: clean build-pi-0 build-pi-1 build-pi-2 build-pi-3 build-pi-4 build-pi-5

# ======================================================================================================================
# BUILD THE C IMAGES
# ======================================================================================================================
build-pi-0: compile-pi-0
	$(CC32) $(CPU_P1) $(PLATFORM_32_BIT) $(CFLAGS) -T ../boot/linker-aarch32.ld -o build/kernel-pi-0.elf build/aarch32-multi-core.o build/kernel-pi-0.o  $(CPPFLAGS)
	$(OBJCOPY32) build/kernel-pi-0.elf -O binary build/kernel-pi-0.img

build-pi-1: compile-pi-1
	$(CC32) $(CPU_P1) $(PLATFORM_32_BIT) $(CFLAGS) -T ../boot/linker-aarch32.ld -o build/kernel-pi-1.elf build/aarch32-multi-core.o build/kernel-pi-1.o  $(CPPFLAGS)
	$(OBJCOPY32) build/kernel-pi-1.elf -O binary build/kernel-pi-1.img

build-pi-2: compile-pi-2
	$(CC32) $(CPU_P2) $(PLATFORM_32_BIT) $(CFLAGS) -T ../boot/linker-aarch32.ld -o build/kernel-pi-2.elf  build/aarch32-single-core.o build/kernel-pi-2.o $(CPPFLAGS)
	$(OBJCOPY32) build/kernel-pi-2.elf -O binary build/kernel-pi-2.img

build-pi-3: compile-pi-3
	$(CC64) $(CPU_P3) $(PLATFORM_64_BIT) $(CFLAGS) -T ../boot/linker-aarch64.ld -o build/kernel-pi-3.elf -nostdlib build/aarch64-single-core.o build/kernel-pi-3.o $(CPPFLAGS)
	$(OBJCOPY64) build/kernel-pi-3.elf -O binary build/kernel-pi-3.img

build-pi-4: compile-pi-4
	$(CC64) $(CPU_P4) $(PLATFORM_64_BIT) $(CFLAGS) -T ../boot/linker-aarch64.ld -o build/kernel-pi-4.elf -nostdlib build/aarch64-single-core.o build/kernel-pi-4.o $(CPPFLAGS)
	$(OBJCOPY64) build/kernel-pi-4.elf -O binary build/kernel-pi-4.img

build-pi-5: compile-pi-5
	$(CC64) $(CPU_P5) $(PLATFORM_64_BIT) $(CFLAGS) -T ../boot/linker-aarch64.ld -o build/kernel-pi-5.elf -nostdlib build/aarch64-single-core.o build/kernel-pi-5.o $(CPPFLAGS)
	$(OBJCOPY64) build/kernel-pi-4.elf -O binary build/kernel-pi-5.img

# ======================================================================================================================
# COMPILE THE C CODE
# ======================================================================================================================
compile-pi-0: boot-32
	$(CC32) $(CPU_P1) $(PLATFORM_32_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-0.o -DRASPBERRY_MODEL_0 $(CPPFLAGS)

compile-pi-1: boot-32
	$(CC32) $(CPU_P1) $(PLATFORM_32_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-1.o -DRASPBERRY_MODEL_1 $(CPPFLAGS)

compile-pi-2: boot-32
	$(CC32) $(CPU_P2) $(PLATFORM_32_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-2.o -DRASPBERRY_MODEL_2 $(CPPFLAGS)

compile-pi-3: boot-64
	$(CC64) $(CPU_P3) $(PLATFORM_64_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-3.o -DRASPBERRY_MODEL_3 $(CPPFLAGS)

compile-pi-4: boot-64
	$(CC64) $(CPU_P4) $(PLATFORM_64_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-4.o -DRASPBERRY_MODEL_4 $(CPPFLAGS)

compile-pi-5: boot-64
	$(CC64) $(CPU_P5) $(PLATFORM_64_BIT) $(CFLAGS) -c ../code/kernel.c -o build/kernel-pi-5.o -DRASPBERRY_MODEL_5 $(CPPFLAGS)

# ======================================================================================================================
# COMPILE THE BOOTLOADERS
# ======================================================================================================================
boot-64:
	$(CC64) $(PLATFORM_64_BIT) $(CFLAGS) -c ../boot/aarch64-single-core.s -o build/aarch64-single-core.o
	$(CC64) $(PLATFORM_64_BIT) $(CFLAGS) -c ../boot/aarch64-multi-core.s -o build/aarch64-multi-core.o

boot-32:
	$(CC32) $(CPU_P1) $(PLATFORM_32_BIT) $(CFLAGS) -c ../boot/aarch32-single-core.s -o build/aarch32-single-core.o
	$(CC32)  $(CPU_P2) $(PLATFORM_32_BIT) $(CFLAGS) -c ../boot/aarch32-multi-core.s -o build/aarch32-multi-core.o

# ======================================================================================================================
# CLEAN
# ======================================================================================================================
clean:
	rm -rf build
	mkdir build

# ======================================================================================================================
# RUN EMULATOR
# ======================================================================================================================
qemu-pi-0: clean build-pi-0
	qemu-system-arm -m 512 -M raspi0 -serial stdio -kernel build/kernel-pi-0.elf

qemu-pi-1: clean build-pi-1
	qemu-system-arm -m 512 -M raspi1ap -serial stdio -kernel build/kernel-pi-1.elf

qemu-pi-2: clean build-pi-2
	qemu-system-arm -m 1024 -M raspi2b -serial stdio -kernel build/kernel-pi-2.elf

qemu-pi-3: clean build-pi-3
	qemu-system-aarch64 -m 1024 -M raspi3b -serial stdio -kernel build/kernel-pi-3.elf
