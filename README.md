# The Raspberry Pi Hello world kernel in gcc, llvm or zig

In this C project we compile, build and emulate a barebone (without an OS) hello world on all the Raspberry Pi models.
This project is primary based on the guides and documentation from:
- [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/getting-started.html)
- [osdev - Raspberry Pi Bare Bones](https://wiki.osdev.org/Raspberry_Pi_Bare_Bones)
- [Processors - Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/processors.html)


## Set up the toolchain
This project can be compiled with the C compilers of [arm-gcc](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads), [llvm](https://llvm.org) and [zig](https://ziglang.org).
The emulation is done with [qemu](https://www.qemu.org).

To install the toolchain on Windows we will use [scoop](https://scoop.sh):

```shell
scoop install gcc-arm-none-eabi llvm zig zls extras/vcredist2022 qemu make
```

To install the toolchain on MacOs we will use [brew](https://brew.sh):

```shell
brew install gcc-arm-embedded aarch64-elf-gcc aarch64-elf-binutils llvm zig zls qemu
```

## Building and running hello world
As the title suggest we can compile the code with gcc `cd gcc && make`,
run the code with `make qemu-pi-2` (or `qemu-pi-0`, `qemu-pi-1`, `qemu-pi-3`)

Or you can compile the code using llvm `cd llvm && make`,
run the code with `make qemu-pi-2` (or `qemu-pi-0`, `qemu-pi-1`, `qemu-pi-3`)

And as last compile the code using zig `cd zig && make`,
run the code with `make qemu-pi-2` (or `qemu-pi-0`, `qemu-pi-1`, `qemu-pi-3`)

## Issues

The current issues in the project are:
- qemu doesn't support the raspberry pi 4 and 5 (is coming soon)
- gcc compile to aarch64 not working on Windows
