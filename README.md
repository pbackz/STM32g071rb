# `cortex-m0 for stm32go71rb`

> A template for building applications for ARM Cortex-M0 microcontrollers

## Target specifying and project build 

``` console
$ rustup target add cargo build --target thumbv7m-none-eabi
$ cargo build --target cargo build --target thumbv7m-none-eabi
$ cargo build
```

0. Before we begin you need to identify some characteristics of the target
  device as these will be used to configure the project:

- The ARM core. e.g. Cortex-M3.

- Does the ARM core include an FPU? Cortex-M4**F** and Cortex-M7**F** cores do.

- How much Flash memory and RAM does the target device has? e.g. 256 KiB of
  Flash and 32 KiB of RAM.

- Where are Flash memory and RAM mapped in the address space? e.g. RAM is
  commonly located at address `0x2000_0000`.

- 128 KiB of Flash located at address 0x0800_0000.

- 36 KiB of RAM located at address 0x2000_0000. (There's another RAM region but
  for simplicity we'll ignore it).

1. Instantiate the template.

``` console
$ cargo generate --git https://github.com/rust-embedded/cortex-m-quickstart
 Project Name: stm32g071rb
 Creating project called `stm32g071rb`...
 Done! New project created /tmp/stm32g071rb

$ cd app
```

2. Set a default compilation target. There are four options as mentioned at the
   bottom of `.cargo/config`. For the STM32F303VCT6, which has a Cortex-M4F
   core, we'll pick the `thumbv7em-none-eabihf` target.

3. Enter the memory region information into the `memory.x` file.

``` console
$ cat memory.x
/* Linker script for the STM32F303VCT6 */
MEMORY
{
  /* NOTE 1 K = 1 KiBi = 1024 bytes */
  FLASH : ORIGIN = 0x08000000, LENGTH = 128K
  RAM : ORIGIN = 0x20000000, LENGTH = 36K
}
```

4. Build the template application or one of the examples.

``` console
$ cargo build
```

# License

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  http://www.apache.org/licenses/LICENSE-2.0)

- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

