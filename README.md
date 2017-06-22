# HiFive1-UART
Quick implementation of a UART interface for [SiFive's FE310 chip](https://www.sifive.com/products/freedom-e310/), as used on the [HiFive1 dev board](https://www.sifive.com/products/hifive1/).

## Usage

Checkout the [freedom-e-sdk](https://github.com/sifive/freedom-e-sdk "Freedom Everywhere SDK") and move
_demo\_uart_ to freedom-e-sdk/software (or clone directly in place). _Make_ as usual with the SDK to build and upload
to target development board:

```bash
dave@Prospero:~/freedom-e-sdk$ make software PROGRAM=demo_uart BOARD=freedom-e300-hifive1
dave@Prospero:~/freedom-e-sdk$ make upload PROGRAM=demo\_uart BOARD=freedom-e300-hifive1
```

## Usage

```c
#include "UART_driver.h"
```

Initialisation:

```c
void UART_init(unsigned long baud, int stop_bits);
```

Deinitialisation:

```c
void UART_deinit();
```

Write a string with option to block program until completed:

```c
int UART_write(char * msg, int blocking);
```

Read input into a target buffer with options for controlling the number of characters to read, which character to stop reading on (typically \n or \r) and specify whether to block:

```c
int UART_read_n(char * buffer, int max_chars, char terminator, int blocking);
```

## Files

+ demo_uart.c: Quick and dirty demonstration. Sets up the UART for 9600 baud and a timer to print a message every second.
+ UART_driver.c: Implementation.
+ UART_driver.h: Include.
+ Makefile: Adds functionality specific to this demo. Note that it's not standalone and relies on including other Makefiles from the SDK.

