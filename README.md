Extra MCU support for Arduino IDE
=================================

This add support for several Microcontrollers recently added by Arduino Team in Arduino IDE.
Here's the list of Microcontrollers:
ATMega1284P
ATMega644P
ATTiny45
ATTyny85
ATTyny44
ATTyny84

Currently only ATMega1284P has been extensively tested and worked well in all situations. I've maded several changes to let
port manipulation easy and compatible with optimizations (aka direct port handle) I've used in my library but also let user
(in almost all cases) to use standard port manipulation tricks used for popular ATMega328P.


INSTALLATION:
First, your Arduino IDE should not running!
Just add the new folders in <b>hardware/arduino/bootloaders</b> and <b>hardware/arduino/variants</b> folders of arduino ide.
You also need to add to your <b>hardware/arduino/boards.txt</b> file the content of this boards.txt file.

 - Bootloaders:
 
ATMega1284P case:
The DIP40 version of this chip it's know to have some problems with UART0 so many people that build a project with this micro
had problems to send sketches, this is not an hardware bug as many supposed but a weird design error of Atmel that put UART pins
to close to Xtal. A common solve to this is add a RC filter to RX0 (100pf from pin 14 to ground and 10K resistor in serie) but
recently a modify on fuse seems to have solved definetively this problem, the fuse has been added to this release.
To install bootloader to ATMega1284P chip I normally use an Arduino UNO or my programmer here on my GitHub page, the procedure it's
exactly the same as program a ATMega328 (just take care of the pins that in 1284P are quite different)

//                         ATMEL ATMEGA644P/1284P
//
//                               +---\/---+
//            PCINT8/(D0 ) PB0  1|        |40  PA0 (A0 / D24)/PCINT0
//            PCINT9/(D1 ) PB1  2|        |39  PA1 (A1 / D25)/PCINT1
//      PCINT10/INT2 (D2 ) PB2  3|        |38  PA2 (A2 / D26)/PCINT2
//      PCINT11/OC0A (D3 ) PB3  4|~       |37  PA3 (A3 / D27)/PCINT3
//   PCINT12/0C0B/SS (D4 ) PB4  5|~       |36  PA4 (A4 / D28)/PCINT4
//      PCINT13/MOSI (D5 ) PB5  6|        |35  PA5 (A5 / D29)/PCINT5
// PCINT14/OC3A/MISO (D6 ) PB6  7|~*      |34  PA6 (A6 / D30)/PCINT6
//  PCINT15/OC3B/SCK (D7 ) PB7  8|~*      |33  PA7 (A7 / D31)/PCINT7
//                         RST  9|        |32  AREF
//                         VCC 10|        |31  GND 
//                         GND 11|        |30  AVCC
//                       XTAL2 12|        |29  PC7 (D23) TOSC2/PCINT23
//                       XTAL1 13|        |28  PC6 (D22) TOSC1/PCINT22
//       PCINT24/RX0 (D8 ) PD0 14|        |27  PC5 (D21) TDI/PCINT21
//       PCINT25/TX0 (D9 ) PD1 15|        |26  PC4 (D20) TDO/PCINT20
//  PCINT26/INT0/RX1 (D10) PD2 16|        |25  PC3 (D19) TMS/PCINT19
//  PCINT27/INT1/TX1 (D11) PD3 17|        |24  PC2 (D18) TCK/PCINT18
//      PCINT28/OC1B (D12) PD4 18|~       |23  PC1 (D17) SDA/PCINT17
//      PCINT29/OC1A (D13) PD5 19|~       |22  PC0 (D16) SCL/PCINT16
//      PCINT30/OC2B (D14) PD6 20|~      ~|21  PD7 (D15) OC2A/PCINT31
//                               +--------+
//
