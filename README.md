# CBM D9096 - a PetSD+ variant
Inspired by the work of Steve J. Gray and his cbmSD-mini, the CBM D9096 is a cost- and feature-reduced version of Nils Eiler's PetSD+ board, designed specifically for headless operation in an external enclosure, connected with a true GPIB cable, similar to a D9060 or D9090.

![CBM 9096 render](https://github.com/InsaneDruid/cbm-d9096/blob/main/images/cbm-d9096_render.png)

[Schematic](https://github.com/InsaneDruid/cbm-d9096/blob/main/cbm-d9096.pdf "Schematic")  

[Bill of Materials](https://htmlpreview.github.io/?https://github.com/InsaneDruid/cbm-d9096/blob/main/bom/cbm-d9096_bom.html "Bill of Materials")

## The Firmware
The CBM D9096 uses the standard petSD+ version of the NODISKEMU firmware.

## The features
A 24-pin Centronics IEEE488/GBIP connector allows the CBM D9096 to be placed anywhere in the IEEE488 chain. This also eliminates the need for a second connector, as the IEEE488 connectors are designed to be stackable.
The SD-Card interface, the status LED and the RESET Button are implemented as pinheaders, so that the main PCB with the GBIB plug and power port can be spaced away from the parts the user needs to interact with, giving flexibility in the design of a case. Additionally, the option to use a Molex Mini Fit Jr Power Plug for connecting to an internal power supply has been implemented.

## The features that got removed
The display with its display controller, the clock, the clock battery, the buttons for interfacing with the display, and the IEC connector have been removed. The circuitry to support SD cards (mainly the 3.3 V power regulator) has also been moved to the readily available card modules. This allows the use of SD and MicroSD modules and the aforementioned flexibility in positioning these modules in a housing.

## The printable housing option
To adapt the cheaply available Bahar enclosue 150*140*70mm project box, 3d printable parts are available.

![Case render](https://github.com/InsaneDruid/cbm-d9096/blob/main/images/case_render.png)
[Printable parts on printables.com](https://www.printables.com/model/878141-cbm-d9069/ "Printable parts on printables.com")  

## The License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.  
See https://creativecommons.org/licenses/by-sa/4.0/.

## The Credits
This work would not have been possible without the work of Nils Eilers and his wonderful PetSD+. In addition, Steve J. Gray had the idea of a similar cost- and feature-reduced version of the PetSD+ when he designed his cbmSD-mini, which uses board-edge connectors and is designed to connect directly to the PETs board and case. This work inspired the CBM D9096.
