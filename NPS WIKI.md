This is the beginning of the new wave of documentation for NPS.
___
# System Overview
- [[PAL]]
- [[DAD]]
- [[DCM]]
- [[BARD]]
# Key Terms

## *Hertz `Hz`*
> - **S.I.** Unit for frequency.
> - Represents `cycles` per `second`.
> ## $$f = \frac{1}{T} = \frac{v}{\lambda} = \frac{\omega}{2\pi}$$
> ![[sine_freq.gif]]
## *310 `MHz`:*
> - Radio Frequency of `310,000,000 Hz` [[#Hertz `Hz`]]
> - Used for Alarms, Tracking, and other local-area communications.
> - For our purposes it has a range of`50ft-300ft` through walls.
> - Transmitted by the [[PAL]] and similar products.
> - Received and decoded by the [[DAD]].
## *IF:*
> - **Intermediate Frequency** is a frequency that is more useful and stable for data decoding and processing.
> - A circuit like a [[DAD]] receives a carrier wave in the form of RF and converts it to an intermediate frequency.


## *Bit-Banging:*
> - A term for any data transfer process where software is used to decode serial information instead of hardware.
## *PIC16F84:*
> - The 18-pin MicroChip Controller used in the [[PAL]].
> - Serves as the brain of the circuit.
> - Responsible for managing the LED, Transmitter, and buttons.
> - See more at [MicroChip's Website](!https://www.microchip.com/en-us/product/pic16f84)
> - Data Sheet - [[pic16f84.pdf]]
> - ![[picpinout.png]]

---

## *BSS84:*
> - P-Channel Enhancement [[#MOSFET]]
> - Used in the [[PAL]] for power control.
> - Pins:
> 	- **Source:** Input terminal.
> 	- **Drain:** Output terminal.
> 	- **Gate:** Control terminal.
> - Allows electricity to flow between **Source** and **Drain** when **Gate** has negative voltage / **Ground**.
## *MMT3904:*
> - NPN [[#Bipolar-Junction-Transistor]].
> - Used in the [[PAL]] for power control.
> - Pins:
> 	- **Collector:** Input Terminal.
> 	- **Emitter:** Output Terminal.
> 	- **Base:** Control Terminal.
> - Allows electricity to flow between **Collector** and **Emitter** as **Base**'s current goes higher.

## *BAV70:*
> - Fast switching Dual-[[Diode]] with a common cathode configuration.
> - Essentially 2 [[Diode]]s connected to the same drain.
> - Pins:
> 	- Terminal A: Input voltage 1.
> 	- Terminal B: Input voltage 2.
> 	- Terminal C:  Output voltage.
> - Limits voltage A->C, and B->C.