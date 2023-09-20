---
tags:
  - Product
---
## [GitHub](https://github.com/National-Protective-Systems/PAL.git)
---
## Description:
- The PAL is a [[NPS WIKI#310 MHz|310 MHz]] Transmitter that sends Panic Alarm signals to the [[DAD]]s located around the site. 
- When pressed, the PAL transmits its serial number, and some additional information to the system.
	- This is used to determine which PAL was pressed, and therefore who needs help.
- The PAL can be tested using a [[PAL Tester]] to determine it's Battery Life and functionality.
- These are made in house and have unique serial numbers for user profiling.
___
## Circuit Design
* Files
	* [[PCB.pdf]]
	* [[SCH1.pdf]]
	* [[SCH2.pdf]]
- The PAL is a very interesting circuit.
- The PAL's circuit starts with +12V connected to...
	- a [[NPS WIKI#BSS84|BSS84]]'s **Source**. ^f64c42
	- a `47 KOhm` resistor.
	- the **Gate** of the [[NPS WIKI#BSS84|BSS84]].
	- a [[NPS WIKI#MMT3904|MMT3904]]'s collector.
		- whose Base is controlled by **-PWR_HOLD** an output pin from the [[NPS WIKI#*PIC16F84 *|PIC16F84]].
		- This allows us to control when the device receives power via the [[#Code]].
			- Specifically: Allows us to keep power on until we are done.
	- a Button **-Panic**.
		- This is also connected to an Input pin on the [[NPS WIKI#*PIC16F84 *|PIC16F84]]
		- Uses a [[NPS WIKI#*BAV70 *|BAV70]] for draining voltage from 2 sources.
	- a Button **-Test**.
		- This is also connected to an Input pin on the [[NPS WIKI#*PIC16F84 *|PIC16F84]]
		- Uses a [[NPS WIKI#*BAV70 *|BAV70]] for draining voltage from 2 sources.
	- a Serial Connection **-Data**.
		- This connection has 2 pin holes. 
		- When connected to a wire it also pulls the voltage down which acts as a button press.
		- This is also connected to an Input pin on the [[NPS WIKI#*PIC16F84 *|PIC16F84]]
		- Uses a [[NPS WIKI#*BAV70 *|BAV70]] for draining voltage from 2 sources.
		- This setup allows the serial connection to enable power the PAL, and transfer information over it via [[NPS WIKI#**Bit-Banging **|Bit-Banging]].
- This setup sends power to the rest of the circuit when a button is pressed because it completes the circuit to ground, which drops the voltage on the [[NPS WIKI#BSS84|BSS84]]
---
## Code
 * For full source code please see the [GitHub](https://github.com/National-Protective-Systems/PAL.git)
- The code for the PAL is stored and ran by the [[NPS WIKI#*PIC16F84 *|PIC16F84]]. 
- This device allows us to run code that controls which wires get power, when, and why.
- The code is responsible for...
	- Determining what button or serial connection was pressed or used.
	- Flashing the LED in certain patterns for User Feedback.
	- Receiving + Storing a serial number and configuration data over the **-Data** wire.
	- Transmitting the serial number and the function code from [[EEPROM]].
- The code is written in Assembly for the [[NPS WIKI#*PIC16F84 *|PIC16F84]].
	- This is an outdated approach and most use [[XC8]] now.

## Programmer:
- In order to program a PAL you need a special tool called a [[PICKIT3.]]
	- This tool is used to load a [[.HEX]] file into a [[NPS WIKI#*PIC16F84 *|PIC16F84]]
- There are 5 pins that connect from the [[PICKIT3.]] to a PAL.
	- These are located on the back-side of the PAL, with the LED pointed down, and the resonator pointed up.

![[PICKit3-Pinout.png]]

| Pin# | PICKIT3 | 
| ---- | ------- |
| 1    | MCLR    | 
| 2    | VDD +   | 
| 3    | VSS -   | 
| 4    | PGD     |
| 5    | PGC     | 

![[palback.jpeg]]
This Table and diagram goes Left-to-Right

| Pin# | PAL   |
| ---- | ----- |
| 1    | VDD + |
| 2    | VSS - |
| 3    | MCLR  |
| 4    | PGC   |
| 5    | PGD   |
