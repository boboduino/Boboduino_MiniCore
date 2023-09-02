# Boboduino MiniCore
[![Build Status](https://travis-ci.com/MCUdude/MiniCore.svg?branch=master)](https://travis-ci.com/MCUdude/MiniCore) [![MiniCore forum thread](https://img.shields.io/badge/support-forum-blue.svg)](https://forum.arduino.cc/index.php?topic=412070.0)

## What is Boboduino Uno R3?
**`Boboduino Uno R3`** is a microcontroller board that is compatible with the popular Arduino Uno R3 board. It is a versatile and feature-packed board that allow makers and developers to easily create and program various electronic projects. The board has multiple power input options, including a **`Type-C USB connector`**, a **`5V JST port`**, or a **`3.7V lithium battery connector`**, and features a **`5V/3.3V power source switch`**, giving users more flexibility in their design. By adapting the **`Atmega 328PB chip`**, the board also comes with extra IIC, serial, and SPI ports, allowing users to connect more devices and sensors. Boboduino has a unique and playful robot layout, making it a great gift idea for makers and tech enthusiasts.

---
## What is Boboduino MiniCore?
* Boboduino MiniCore is an Arduino core modified from profound [MiniCore](https://github.com/MCUdude/MiniCore) tailored for the Boboduino Uno R3 board. 
* It is basically a simplified version of MiniCore which make the options to choose McU other than the Atmega 328 series to be hidden.It is much more suitable for both the Boboduino board and beginners.
* Once you have reach to the level of **`Bobo master`** and you want to tweak or explore more, you can always install the lovely [MiniCore](https://github.com/MCUdude/MiniCore). It can also be used with the Boboduino Uno R3 board.

---

# Table of contents
** Ignore the advance part if you just want to simply install the core for microcontroller learning**
* [System requirement](#system-requirement)
* [How to install](#how-to-install)
	- [Boards Manager Installation (Arduino IDE)](#boards-manager-installation-arduino-ide)
	- [Manual Installation (Arduino IDE)](#manual-installation-arduino-ide)
	- [PlatformIO IDE](#platformio)
* [Bootloader fuse settings(advanced)](bootloader-fuse-settings)
    * [Clock](#supported-clock-frequencies)
    * [BOD option](#bod-option)
    * [EEPROM](#eeprom-option)
    * [Compiler LTO](#link-time-optimization--lto)
    * [Variant]()
    * [Bootloader](#bootloader-option)
* Advance functions
    * [Printf support](#printf-support)
    * [Pin macros](#pin-macros)
    * [Flash writing supports](#write-to-own-flash)
    * [Programmers](#programmers)

* [Supported microcontrollers(advanced)](#supported-microcontrollers)

* **[Getting started with MiniCore](#getting-started-with-minicore)**
* [Wiring reference](#wiring-reference)
* **[Pinout](#pinout)**
* **[Minimal setup](#minimal-setup)**

---
## System requirement
* This core requires Arduino IDE **`v1.8.13+`**.  
* A computer with the installation of Windows, Mac OS or Linux.
* A cute Boboduino Uno R3 board :-).


---

## How to install
### Boards Manager Installation (Arduino IDE)
This installation method requires Arduino IDE version v1.8.13+ or greater.
* Open the Arduino IDE.
* Open the **File > Preferences** menu item.
* Enter the following URL in **Additional Boards Manager URLs**:

    ```
    https://raw.githubusercontent.com/boboduino/Boboduio_MiniCore/master/third-party%20board/package_boboduino.com_index.json
    ```

* Open the **Tools > Board > Boards Manager...** menu item.
* Wait for the platform indexes to finish downloading.
* Scroll down until you see the **Boboduino** entry and click on it.
* Click **Install**.
* After installation is complete close the **Boards Manager** window.
* **Note**: If you plan to use the *PB series, you need the latest version of the Arduino toolchain. This toolchain is available through IDE 1.8.6 or newer. Here's how you install/enable the toolchain:
  - Open the **Tools > Board > Boards Manager...** menu item.
  - Wait for the platform indexes to finish downloading.
  - The top is named **Arduino AVR boards**. Click on this item.
  - Make sure the latest version is installed and selected
  - Close the **Boards Manager** window.

### Manual Core Installation (Arduino IDE)
* Download the core file of [BOBODUINO_MiniCore_2.2.2.zip](https://github.com/boboduino/Boboduio_MiniCore/raw/master/third-party%20board/2.2.2/BOBODUINO_MiniCore_2.2.2.zip).
* Exctract the ZIP file, and move the extracted folder to the location:
    * Windows: `"~/Documents/Arduino/hardware"`. Create the "hardware" folder if it doesn't exist.
    * Mac: `"/Users/cheney/Library/Arduino15/packages"`
* Open Arduino IDE, and a new category in the boards menu called `"Boboduino AVR boards"` will show up.

---
## PlatformIO
* [PlatformIO IDE](https://platformio.org/platformio-ide) is an open source ecosystem for embedding sytem development which is build built on top of Microsoft's [Visual Studio Code](https://code.visualstudio.com)
* Compared to Arduino IDE, it is much more powerful with the debugging features.
* We hightly recommand you to used it when you are planning to build more complex projects.
* Please take a look at [PlatformIO.md](https://github.com/boboduino/Boboduio_MiniCore/blob/master/PlatformIO.md) for more information.

---

## Code uploading
you can upload your code in two ways:

### Upload through USB
* Connect a USB to serial adapter to the microcontroller
* Select the correct `serial port device` under the **Tools>Port** menu, and click the **Upload** button. 
* If you're getting some kind of timeout error, it may be because:
    * RX and TX pins are swapped, 
    * The auto reset circuity isn't working properly (Check if the Auto-reset JP3 solder jumper at the back of the board has been solder and connected).

### Uplaod through external programmer 
* You can burning sketches to the Arduino board with an external programmer.
* This method bypass the bootloader, which can saving program space on the chip.
* Use the option **Sketch > Upload Using Programmer**, this will erase the bootloader and upload your code using the programmer tool.
* Further reading: [Burning sketches to the Arduino board with an external programmer](https://docs.arduino.cc/hacking/software/Programmer).

Your code should now be running on your microcontroller! If you experience any issues related to bootloader burning or serial uploading, please use *[this forum post](https://forum.arduino.cc/index.php?topic=412070.0)* or create an issue on Github.

---



# Bootloader settings **`[Advanced]`**
The Boboduino MiniCore bootloader has **DEFAULTLY** been written to your board. However, if you want to re-write the booloader, here's a quick guide you can follow.


## Understand the bootloader setting **`[Advanced]`**
* Connect your Boboduino Uno R3 microcontroller board with the [Arduino as ISP uploader](https://docs.arduino.cc/built-in-examples/arduino-isp/ArduinoISP) or other ICSP uploading board.
* Open the **Tools > Board** menu item, and select `"Boboduino AVR boards"` and `""Boboduino Uno R3"`.

You can adjust the fuse setting from the drop-down menu of  `[Tool]` in yor Arduino IDE. 
* **`[Clock]`**: The clock frequency which the McU is running at. **16 MHz** is standard on Boboduino and most of official Arduino boards. [[Clock]](#clock-running-clock-frequency)
* **`[BOD]`**:  **Brown out detection voltage**, the voltage that microcontroller will shut down at. ([BOD](#bod-option)).
* **`[EEPROM]`**: Wheather to remove the data store in the EEPROM or not. Choose **EEPROM not retained** when you want to cleanup the EEPROM after upload the bootloader. [[EEPROM]]()
* **`[Compiler LTO]`**: Wheather to use the **link time opertimization(LTO)**. LTO optimizes the code at link time, making the code (often) significantly smaller without making it "slower". [[LTO]]()
* **`[Variants]`**: Which microcontroller chip you're using. Boboduino Uno R3 adapt the ATmega 328PB chip.[[Variants]]()
* `**[Bootloader]**`: Which UART(UART0 or UART1) port you want to use to uplaod the code. [[Bootloader]]()

## Re-write the bootloader **`[Advanced]`**
1. Select the programmer: The programmer is the device that you can use to write the bootloader to your board. Select which programmer you're using under the **`[Programmers]`** menu.(For example if you use the [Arduino as ISP](https://docs.arduino.cc/built-in-examples/arduino-isp/ArduinoISP) then just select it!)
2. Burn Bootloader: Hit **`[Burn Bootloader]`**. If an LED is connected to pin PB5 (Arduino pin 13), it should flash twice every second.
The modified fuse setting will be written to the burnt bootloader.
---

## Detail bootloader setting
### [Variants] Supported microcontrollers
* Arudino Uno R3 adapt the ATmega 328P chip, where Boboduino Uno R3 mount the slightly advance [ATmega328PB](https://www.mouser.com/ProductDetail/Microchip-Technology/ATMEGA328PB-AU?qs=jy4bLUHv09hbFONgGrqPbw%3D%3D&_gl=1*1i96pqq*_ga*MTAwNDU1Njk3OC4xNjkzNTQ4NDg2*_ga_15W4STQT4T*MTY5MzU0ODQ4Ni4xLjEuMTY5MzU0ODUxNS4wLjAuMA..*_ga_1KQLCYKRX3*MTY5MzU0ODQ4Ni4xLjEuMTY5MzU0ODUxNS4zMS4wLjA.) chip as the default processer, which is fully compatible with the official Arduino Uno R3 but with some more useful functions. 
* The official MiniCore support lots of ATmega chips. However, we slimmed the function of this part beacuse Boboduino can only use the ATmega 328 series chip.

* Hence, You can only see the option of [ATmega 328PB chip](https://www.mouser.com/ProductDetail/Microchip-Technology/ATMEGA328PB-AU?qs=jy4bLUHv09hbFONgGrqPbw%3D%3D&_gl=1*1i96pqq*_ga*MTAwNDU1Njk3OC4xNjkzNTQ4NDg2*_ga_15W4STQT4T*MTY5MzU0ODQ4Ni4xLjEuMTY5MzU0ODUxNS4wLjAuMA..*_ga_1KQLCYKRX3*MTY5MzU0ODQ4Ni4xLjEuMTY5MzU0ODUxNS4zMS4wLjA.) in the menu of **`[Variants]`** .

### Chip replacement **`[Advanced]`**
* Chip replacement: For advance user, this 328PB chip can also be replaced with other 328 series chip with 32-TQFP package.  To replace the chip, you will need a hot plate or hot gun, soldering paste, and good skill. :-)
* **Bootloader core modificaion**: After you replace the chip, you can remove the comment of `328.menu.variant` in the **board.txt** file of Boboduino MiniCore  and restart the Arduino IDE. The option of other 328 chip will now be seen in the pull-down menu of **Tool>variant**. 

---

### [Clock] Running Clock Freqeuency 
 *This board adpot the **16 MHz** external crystal oscillator. Which is the same as the Arduino Uno R3. 
* The original MiniCore botloader supports a variety of different clock frequencies. However, we intended to restricted it to support only 16 MHz external crystal oscillator to avoid confusion of the options for the beginner.


### Change clock frquency **`[advanced]`**
* You can replace(or remove) the external crystal oscillator with other frequency with the hot plate or hot gun.
* The option of selection other frequency can be turn on by remove the comment of **328.menu.clock** in the file of  **board.txt**. 
* After you remove the commant and restart the Arduino IDE, you can see the option of other frequency at the pull-down menu of **Tool>Clock**.
* Select the target frequncy after you have replaced(or removed) the external clock.
* You'll have to hit "Burn bootloader" in order to set the correct fuses and upload the new bootloader.
* Make sure you connect an ISP programmer, and select the correct one in the "Programmers" menu. For time critical operations an external crystal/oscillator is recommended.

* You might experience upload issues when using the internal oscillator. It's factory calibrated but may be a little "off" depending on the calibration, ambient temperature and operating voltage. If uploading failes while using the 8 MHz internal oscillator you have these options:
* Edit the baudrate line in the boards.txt file, and choose either 115200, 57600, 38400 or 19200 baud.
* Upload the code using a programmer (USBasp, USBtinyISP etc.)
* Use the 4, 2 or 1 MHz option instead

| Frequency   | Oscillator type             | Comment                                                       |
|-------------|-----------------------------|---------------------------------------------------------------|
| 16 MHz      | External crystal/oscillator | Default clock on most AVR based Arduino boards and MiniCore   |
| 20 MHz      | External crystal/oscillator |                                                               |
| 18.4320 MHz | External crystal/oscillator | Great clock for UART communication with no error              |
| 14.7456 MHz | External crystal/oscillator | Great clock for UART communication with no error              |
| 12 MHz      | External crystal/oscillator | Useful when working with USB 1.1                              |
| 11.0592 MHz | External crystal/oscillator | Great clock for UART communication with no error              |
| 8 MHz       | External crystal/oscillator | Common clock when working with 3.3V                           |
| 7.3728 MHz  | External crystal/oscillator | Great clock for UART communication with no error              |
| 4 MHz       | External crystal/oscillator |                                                               |
| 3.6864 MHz  | External crystal/oscillator | Great clock for UART communication with no error              |
| 2 MHz       | External crystal/oscillator |                                                               |
| 1.8432 MHz  | External crystal/oscillator | Great clock for UART communication with no error              |
| 1 MHz       | External crystal/oscillator |                                                               |
| 8 MHz       | Internal oscillator         | Might cause UART upload issues. See comment above this table  |
| 4 MHz       | Internal oscillator         | Derived from the 8 MHz internal oscillator                    |
| 2 MHz       | Internal oscillator         | Derived from the 8 MHz internal oscillator                    |
| 1 MHz       | Internal oscillator         | Derived from the 8 MHz internal oscillator                    |


## [Bootloader] Which UART port to upload the bootloader? 
* Boboduino Uno board support upload the code with `UART0` with the default setting(Which is the same as the offical Arduino Uno R3).
### Erase the bootloader **`[advnced]`**

* If your application doesn't need or require a bootloader for uploading code you can also choose to disable this by selecting *No bootloader*. This frees **512 bytes** of flash memory.
* Unlike official Arduino AVR boards, the bootloader isn't automatically removed when you upload using a programmer. You'll have to select *No bootloader* hit "upload" or the "burn bootloader" for this to happen.
    
### Upload code with UART1 **`[advanced]`**
* 328PB chip has two UART port, `UART0`, `UART1`. 
* `UART0` is the default port for this board(Which is the same as the official Arduino Uno R3).
* To turn on the UART1 code uploading function, you can remove the comment of `328.menu.bootloader.uart1` in the **board.txt** file. 
* You can find the option to select UART1 in the drop-down menu of **Tool>Bootloader** after you restart the Arduino IDE.

Note that you have need to connect a programmer and hit **`Burn bootloader`** if you want to change any of the *Upload port settings*.




## [BOD] Brown down detection
* `**Brown out detection**`, or BOD for short lets the microcontroller sense the input voltage and shut down if the voltage goes below the brown out setting. 
* Like the official Arduino Uno R3, the default setting of brown out detection voltage has to be set to `**2.7v**`.
* To change the BOD settings you'll have to connect an ISP programmer and hit "Burn bootloader". Below is a table that shows the available BOD options:
    * 4.3V
    * **2.7V(default)**
    * 1.8V
    * Disabled


## [EEEPROM] EEPROM erasure
* If you want the EEPROM to be erased every time you burn the bootloader or upload using a programmer, you can turn off this option. 
* You'll have to connect an ISP programmer and hit "Burn bootloader" to enable or disable EEPROM retain. Note that when uploading using a bootloader, the EEPROM will always be retained.


## [Compiler LTO] Link time optimization
* After Arduino IDE 1.6.11 where released, There have been support for link time optimization or LTO for short. 
* The LTO optimizes the code at link time, making the code (often) significantly smaller without making it "slower".
* In Arduino IDE 1.6.11 and newer LTO is **enabled by default**.
* I've chosen to disable this by default to make sure the core keep its backwards compatibility. 
* Enabling LTO in IDE 1.6.10 or older will return an error.
* I encourage you to try the new LTO option and see how much smaller your code gets! Note that you don't need to hit "Burn Bootloader" in order to enable LTO. Simply enable it in the "Tools" menu, and your code is ready for compilation. 
* If you want to read more about LTO and GCC flags in general, head over to the [GNU GCC website](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)!


# Advance functions


## Printf() function support
* Unlike the official Arduino cores, MiniCore has printf support out of the box. 
* If you're not familiar with printf you should probably [read this first](https://www.tutorialspoint.com/c_standard_library/c_function_printf.htm). It's added to the Print class and will work with all libraries that inherit Print. 
* Printf is a standard C function that lets you format text much easier than using Arduino's built-in print and println. **Note that this implementation of printf will NOT print floats or doubles**. 
* This is a limitation of the avr-libc printf implementation on AVR microcontrollers, and nothing I can easily fix.
* If you're using a serial port, simply use `Serial.printf("Milliseconds since start: %ld\n", millis());`. You can also use the `F()` macro if you need to store the string in flash. Other libraries that inherit the Print class (and thus supports printf) are the LiquidCrystal LCD library and the U8G2 graphical LCD library.


## Pin macros
Besides using the Arduino pre-defined digital pin numbers to refer to the pins, tou can also use some `predefined macros that maps "Arduino pins"` to the port and port number:

```c++
// Use PIN_PB5 macro to refer to pin PB5 (Arduino pin 13)
digitalWrite(PIN_PB5, HIGH);

// Results in the exact same compiled code
digitalWrite(13, HIGH);

```

---

## Directly flash memory writing 
* Boboduino MiniCore uses Optiboot Flash, a bootloader that supports flash writing within the running application, thanks to the work of [@majekw](https://github.com/majekw).
* This means that content from e.g. a sensor can be stored in the flash memory directly without the need of external memory. 
* **Flash memory is much faster than EEPROM**, and can handle at least **10,000 write cycles** before wear becomes an issue.
*For more information on how it works and how you can use this in you own application, check out the [Serial_read_write](https://github.com/MCUdude/MiniCore/blob/master/avr/libraries/Optiboot_flasher/examples/Serial_read_write/Serial_read_write.ino) for a simple proof-of-concept demo, and
[Flash_put_get](https://github.com/MCUdude/MiniCore/blob/master/avr/libraries/Optiboot_flasher/examples/Flash_put_get/Flash_put_get.ino) + [Flash_iterate](https://github.com/MCUdude/MiniCore/blob/master/avr/libraries/Optiboot_flasher/examples/Flash_iterate/Flash_iterate.ino) for useful examples on how you can store strings, structs and variables to flash and retrieve then afterwards.
The [Read_write_without_buffer](https://github.com/MCUdude/MiniCore/blob/master/avr/libraries/Optiboot_flasher/examples/Read_write_without_buffer/Read_write_without_buffer.ino) example demonstrate how you can read and write to the flash memory on a lower level without using a RAM buffer.

---

## Programmers **`[Advanced]`**
* The official MiniCore adds its own copies of all the standard programmers to the "Programmer" menu. Just select one of the programmer in the "Programmers" menu, and you're ready to "Burn Bootloader" or "Upload Using Programmer".

* To upload the bootloader, after youelect your microcontroller in the **`[boards]`** menu, then select the clock frequency. You'll have to hit "Burn bootloader" in order to set the correct fuses and upload the correct bootloader. <br/>
* Make sure you connect an ISP programmer, and select the correct one in the "Programmers" menu. For time critical operations an external oscillator is recommended.

---
# Wiring reference
To extend this core's functionality a bit further, The original MiniCore has add a few missing Wiring functions. These functions can be used as "regular" Arduino functions, and there's no need to include an external library.<br/>
I hope you find this useful, because they really are!

### Function list
* portMode()
* portRead()
* portWrite()
* sleepMode()
* sleep()
* noSleep()
* enablePower()
* disablePower()

### For further information please view the [Wiring reference page](https://github.com/MCUdude/MiniCore/blob/master/Wiring_reference.md)!


# Design your own board **`[Advanced]`**
Once in the future, you may want to develop your own print circuit board for specific application. Here are some information which may help you to startup your circuit design journey.

## Chip diagram
* The diagram below may help you to quickly know what are the function of each pins of each chip.
* The MinicCore uses the standard Arduino UNO pinout and will not break compatibility of any existing code or libraries. What's different about this pinout compared to the original one is that this got three aditinal IO pins available. 
* You can use digital pin 20 and 21 (PB6 and PB7) as regular IO pins if you're ussing the internal oscillator instead of an external crystal. If you're willing to disable the reset pin (can be enabled using [high voltage parallel programming](https://www.microchip.com/webdoc/stk500/stk500.highVoltageProgramming.html)) it can be used as a regular IO pin, and is assigned to digital pin 22 (PC6).

<b>Click to enlarge:</b>
</br> </br>

| DIP-28 package  *ATmega8/48/88/168/328*               | TQFP-32 SMD package  *ATmega8/48/88/168/328*          | TQFP-32 SMD package  *ATmega48/88/168/328PB*          |
|-------------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
|<img src="https://i.imgur.com/qXIEchT.jpg" width="280">|<img src="https://i.imgur.com/naweqE6.jpg" width="260">|<img src="https://i.imgur.com/ZQsjLwL.jpg" width="260">|


## Minimal setup circutry **`[Advanced]`**

* Here is a simple schematic showing a minimal setup using an external crystal. 
* Skip the crystal and the two 22pF capacitors if you're using the internal oscillator. 
* <b>Click to enlarge:</b> <br/>

| DIP-28 package  *ATmega8/48/88/168/328*               | TQFP-32 SMD package  *ATmega8/48/88/168/328*          | TQFP-32 SMD package  *ATmega48/88/168/328PB*          |
|-------------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
|<img src="https://i.imgur.com/1k4q3xF.png" width="280">|<img src="https://i.imgur.com/bp7KI9f.png" width="280">|<img src="https://i.imgur.com/LrEokO9.png" width="280">|

---

# Generic AVR programming
* As I konw, most of user use Arduino IDE and Platform IO for most of their job. However, if you're into "generic" AVR programming, I'm happy to tell you that all relevant keywords are being highlighted by the IDE through a separate keywords file. Make sure to test the [example files](https://github.com/MCUdude/MiniCore/tree/master/avr/libraries/AVR_examples/examples) (File > Examples > AVR C code examples). Try writing a register name, <i>DDRB</i> for instance, and see for yourself!