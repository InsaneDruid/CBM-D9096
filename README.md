# CBM D9096 - a PetSD+ variant
Inspired by the work of Steve J. Gray and his cbmSD-mini, the CBM D9096 is a cost- and feature-reduced version of Nils Eiler's PetSD+ board, designed specifically for headless operation in an external enclosure, connected with a true GPIB cable, similar to a D9060 or D9090.

![CBM 9096 render](https://github.com/InsaneDruid/cbm-d9096/blob/main/images/cbm-d9096_render.png)

[Schematic](https://github.com/InsaneDruid/cbm-d9096/blob/main/cbm-d9096.pdf "Schematic")  

[Bill of Materials](https://htmlpreview.github.io/?https://github.com/InsaneDruid/cbm-d9096/blob/main/bom/cbm-d9096_bom.html "Bill of Materials")

## The features
A 24-pin Centronics IEEE488/GBIP connector allows the CBM D9096 to be placed anywhere in the IEEE488 chain. This also eliminates the need for a second connector, as the IEEE488 connectors are designed to be stackable.
The SD-Card interface, the status LED and the RESET Button are implemented as pinheaders, so that the main PCB with the GBIB plug and power port can be spaced away from the parts the user needs to interact with, giving flexibility in the design of a case. Additionally, the option to use a Molex Mini Fit Jr Power Plug for connecting to an internal power supply has been implemented.

## The features that got removed
The display with its display controller, the clock, the clock battery, the buttons for interfacing with the display, and the IEC connector have been removed. The circuitry to support SD cards (mainly the 3.3 V power regulator) has also been moved to the readily available card modules. This allows the use of SD and MicroSD modules and the aforementioned flexibility in positioning these modules in a housing.

## The SD card adapters - 1.1.0 adding more options
The board now features two headers to attach readily available SD card and Micro SD card modules.
The one marked *5V SPI SD-CARD* (J3) is operating at 5 volts! The card modules attached here  MUST have appropriate level shifters installed.
Tis applies to nearly all readily available Micro SD card modules, but only some older SD card modules.
Tested and working boards are: *DEBO MICROSD 2* and *C-Control Pro Nr. 197220*
Boards that just use a voltage regulator and some passive resistors do NOT work on this header!

The one marked *3.3V SPI SD-CARD* (J5) is operating at 3.3 volts using a TXU0304 SPI level shifter and a 3.3V regulator.The card modules attached here don't need (and should *not* have!) their own level shifters.
This applies to nearly all readily available full size SD card modules. Note: this port supplies 3.3V OR 5V to the card module. Select the appropriate pin depending on the card module to connect. 

*Attention!* you CANNOT install two SD card modules at the same time!

## The *card detect* and *write protect* signals
Both SD card headers J3 & J5 have ground pin headers available behind the pins for the card detect ("CD") and write protect ("WP) signals (marked J4 & J6). If the attached card module doesn't provide these signals, for example all Micro SD modules, connect a 2.54mm jumper between the CD and or WP pins of J3/J5 and the associated pin of J4/J6 to permanently tie these signals to ground (permanently enable them).

## The Firmware
Andy Grady has provided a customized [firmware](https://github.com/InsaneDruid/cbm-d9096/blob/main/firmware/cbm-d9096.bin "cbm-d9096.bin") in which the button input is completely deactivated, so that the use of a voltage divider and filtered analog voltage is no longer necessary and with V1.1.0 these supporting parts are omitted. 

### Firmware installation
* Flash the [bootloader](https://github.com/InsaneDruid/cbm-d9096/blob/main/firmware/new-bootloader-for-16-MHz-petSD-plus.hex "new-bootloader-for-16-MHz-petSD-plus.hex") file to the Atmega. 
    * Set the fuse bits to Low: F7, High: D2, Extended: FC
        * low: CKSEL3=low
        * high: SPIEN=0, EESAVE=0, BOOTSZ1=0, BOOTRST=0
        * extended: BODLEVEL1=0, BODLEVEL0=0
* Install the Atmega in the board.
* Copy the [firmware](https://github.com/InsaneDruid/cbm-d9096/blob/main/firmware/cbm-d9096.bin "cbm-d9096.bin") to a FAT16 or FAT32 formatted SD-card.
* Insert the prepared card and turn on the d9096.
* On startup, the bootloader will program the firmware to the Atmega.
    * The file name is not important - the bootloader checks for a hardware tag and version number in the file.
    * During the flash operation the busy LED flickers rapidly.
    * If a valid firmware is not found, the boot loader will flash the error LED for two seconds and try to find a valid file once more.

## The LED options
The board is designed to be configured for a 2 LED or 3 LED setup:

### 2 LED variant
In the 2 LED variant power and error are combined in a *bidirectional* dual-color led (NOT common cathode or common anode!), reminiscent of how the CBM drives did. Activity is shown on a standard LED.

* install a jumper wire in place of R2
* connect a bidirectional LED between pins 3 (error) and 4 (power) of J2
* connect a standard LED between pins 1(activity) and 2 (gnd) of J2

### 3 LED variant
In the 3 LED variant power and error as well as activity are displayed with independent LED.

* don't install R4 (leave open)
* install a 330 Ohm resistor in R1, R2, R3
* connect power LED between pins 4 (power) and 2 (GND) of J2
* connect error LED between pins 3 (error) and 2 (GND) of J2
* connect activity LED between pins 1 (activity) and 2 (GND) of J2

## The printable housing option
To adapt the cheaply available Bahar enclosue 150*140*70mm project box, 3d printable parts are available.

![Case render](https://github.com/InsaneDruid/cbm-d9096/blob/main/images/case_render.png)
[Printable parts on printables.com](https://www.printables.com/model/878141-cbm-d9069/ "Printable parts on printables.com")  

## The License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.  
See https://creativecommons.org/licenses/by-sa/4.0/.

## The Credits
This work would not have been possible without the work of Nils Eilers and his wonderful PetSD+. In addition, Steve J. Gray had the idea of a similar cost- and feature-reduced version of the PetSD+ when he designed his cbmSD-mini, which uses board-edge connectors and is designed to connect directly to the PETs board and case. This work inspired the CBM D9096.

Special thanks also go to Andy Grady for the customized firmware.
