# AVR-Xminis (Debug enabled)

This is a debug-enabled Arduino core for the Microchip development boards

- [ATmega328P Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega328p-xmini),
- [ATmega168BP Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega168pb-xmini), and
- [ATmega328PB Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega328pb-xmini).

These boards contain an embedded debugger and programmer, and their footprint is compatible with the Arduino Uno R3 board. So, you can connect any Uno shield to it. Since there is now a [cross-platform debugging solution for the Arduino IDE 2](https://github.com/felias-fogg/PyAvrOCD/), the Xplained Minis are ideal for developing Arduino applications. And these boards are also very affordable. 

## The Core

There exists an Arduino platform definition from Atmel from 10 years ago for these boards as part of the standard Arduino distribution. However, it appears to be completely outdated. For this reason, I based this implementation on [MCUdude's MiniCore](https://github.com/MCUdude/MiniCore), which contains a few nice additions, such as `printf`. Actually, you could simply use MiniCore, but then you need to adjust all the bells and whistles, and there are a few tricky corners to navigate. With this new core, you can simply start after selecting the board. 

## Selecting a board in the IDE

The most convenient way to select a board in the IDE 2 is to use the drop-down list from the `Select Board` field at the top of the Arduino IDE 2 window after the board has already been plugged in. One entry should read `Unconfirmed board`. If you choose that, you get a list of possible boards. If it does not show, search for `xp`. There you can select the right board. At the same time, the IDE connects to the serial connection on the board that can be used for `Serial Monitor` interaction.

## Setting board parameters

After having chosen the board, you can adjust three board parameters:

- `Clock`: Here you can specify whether the clock runs at 8 MHz or 16 MHz (default). The lower frequency can be achieved when the board is powered with 3.3 V. How to accomplish that is described in the hardware description of the board (see link above). The value of this parameter is essential for the compilation process because the timing of the compiled code depends on the CPU clock frequency. However, note that changing the value of this parameter alone will *not* change the clock frequency!
- `EEPROM`: Here, you can choose whether EEPROM content should be deleted or retained when reprogramming the chip. Once you have done that, you need to run the `Burn Bootloader` action in the `Tools` menu. This will set the appropriate fuse (but will not burn a bootloader, which is not required anyway).
- `Compiler LTO`: This parameter controls whether link-time optimization should be applied in the compilation and link process. If enabled (which is the default), the generated machine code can be significantly smaller. However, this kind of optimization will also remove important debugging information and will, in particular, make global variables invisible in the variable pane. 

## Getting started

Before starting to debug, one should activate the `Optimize for Debugging` entry in the `Sketch` menu. After that, one can upload the code to the board and then press the debug button. No other preparations are necessary to begin debugging—no solder bridges to cut or confusing fuses to set. And entering and leaving debugWIRE mode is fully automated without manual power-cycling or typing any funny commands. In fact, you probably will not notice that you have to deal with debugWIRE.

## Minimizing upload time

It is not strictly necessary to upload the code before starting debugging. One could simply compile it using the `Verify` button. The code will usually be loaded at the beginning of the debugging session anyway, but at a much slower speed. If the code is already uploaded, the debugger will only verify that the code is there, which is much faster. If you want to optimize this verification process away as well, you can place the file `pyavrocd.option` containing the single line `--load=cacheonly` into the sketch folder. This will load the code only into the cache and prohibit the verification process.  

## The power of the ATmega328PB

Note that the ATmega328PB has a few additional features, such as two additional PWM pins, a second hardware serial peripheral (`Serial1`), a second TWI peripheral (`Wire1`), and a second SPI peripheral (`SPI1`), four additional GPIO pins (PE0-PE4, respectively, Arduino D23-D26), and two extra 16-bit timers (Timer/Counter3 & 4). See also the [hardware comparison](https://onlinedocs.microchip.com/oxy/GUID-CBDC1838-0100-4F26-A45A-134958193C3B-en-US-4/index.html) by Microchip.

