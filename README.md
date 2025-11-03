# AVR-Xminis

This is an Arduino core for the Microchip boards

- [ATmega328P Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega328p-xmini),
- [ATmega168BP Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega168pb-xmini), and
- [ATmega328PB Xplained Mini](https://www.microchip.com/en-us/development-tool/atmega328pb-xmini).

These boards contain an embedded debugger and programmer, and their footprint is compatible with the Arduino Uno R3 board. So, you can plug any Uno shields on it. Since there is now a [cross-platform debugging solution for the Arduino IDE 2](https://github.com/felias-fogg/PyAvrOCD/), the Xplained Minis are ideal for developing Arduino applications. And these boards are also very affordable. 

After installing this core, you can program and upload Arduino sketches immediately. No preparations are necessary to begin debugging—no solder bridges to cut or confusing fuses to set. And entering and leaving debugWIRE mode is fully automated.

Well, one should activate the `Optimize for Debugging` entry in the `Sketch` menu. After that, one can upload the code to the board and then press the debug button. Actually, it is not strictly necessary to upload the code before starting debugging, because it will be loaded at the beginning of the debugging session anyway, but at a much slower speed. If the code is already uploaded, however, the debugger will only verify that the code is there, which is much faster.

There is an Arduino platform definition from Atmel from 10 years ago for these boards. However, it is completely outdated. For this reason, I based this implementation on [MCUdude's MiniCore](https://github.com/MCUdude/MiniCore), which contains a few nice additions, such as `printf`. Actually, you could simply use MiniCore, but then you need to adjust all the bells and whistles, and there are a few tricky corners to navigate. With this core, you can simply start after selecting the board. Otherwise, programming is similar to using an UNO. Note that the ATmega328PB has a few additional features, such as more PWM outputs, a second hardware serial peripheral (`Serial1`), a second TWI peripheral (`Wire1`), and a second SPI peripheral (`SPI1`), four additional GPIO pins (PE0-PE4, respectively, Arduino D23-D26), and two extra 16-bit timers (Timer/Counter3 & 4). See also the [hardware migration guide](https://onlinedocs.microchip.com/oxy/GUID-CBDC1838-0100-4F26-A45A-134958193C3B-en-US-4/index.html) by Microchip.

