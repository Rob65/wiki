# LoRa hardware - Nodes

## Short note on hardware development
Below is technical information on various options for developing your own
Internet of Things node. If you've never done hardware development before,
you might want to start with some online resources first.
Have a look at the free [IoT introduction courses on coursera](https://www.coursera.org/specializations/iot).
(Note that the courses are freely accessible by searching for the course names
on Coursera.org.) Some background in programming both Arduino's and Raspberry
Pi's will greatly help prototyping your own IoT devices. There's many more
resources available on connecting particular hardware components to Arduino-compatible
microcontrollers, for example [this Sparkfun introduction](https://learn.sparkfun.com/tutorials/what-is-an-arduino),
[ladyada's tutorial](http://www.ladyada.net/learn/arduino/) and the
official practical [Arduino introductory booklet](https://store.arduino.cc/product/B000001).


## Supported Hardware
Like WiFi and 3G/4G, LoRa connections need specific hardware
support for connections. Since the technology is only gaining
traction now, most devices won't support it (yet). In the near
future (2016/2017) commercial devices might hit the market.
For now, you'll need to build (or buy) devices yourself.


## Node summary
There's at least ten providers selling breakout boards for
LoRa(WAN) nodes. All of them use the SX1272 or SX1276 chip,
produced by SemTech and providing the 'raw' LoRa hardware
protocol. 

A **node** has two building blocks. a communication part and a calculation part. 

**Communication** is done via the SX1272 or SX1276 chip this is the modem part of the node. 
**Calculation** is done by a separate [MCU](https://www.quora.com/What-is-the-difference-between-a-microprocessor-and-microcontroller) like  an Arduino or ARM Cortex.
The LoRaWAN software stack needs to run on the MCU (the calculation part)
Some boards include a MCU, some don't and just provide the modem interface of the chip. 
There are bare breakout boards, Bee connectors, or all-included development boards. There are a few different implementations, and they're not yet all compatible with each other.

To get started building a node, see our **[Hardware Nodes Overview](Hardware/OverviewNodes)**.
This includes hardware, software and how to buy or build it.


## Overview
Here's a table of a few hardware boards supporting LoRa.
Specific instructions can be found below. If you're unsure
what to buy, send us an [email](Contact).

| Device            | | Chip   | | MCU          || Connector   || Cost (EUR)   || Comments                   |
| ----------------- |-| ------ |-| ------------ || ----------- || -------------|| -------------------------- |
| Sodaq Tatu + Bee  | | LR1272 | | ATMega 1284P || Bee         || 35,- + 35,-  || Arduino-IDE compatible     |
| Sodaq Mbili + Bee | | RN2483 | | ATMega 1284P || Bee         || 98,-         || Arduino-IDE compatible     |
| Kickst. TTN Uno   | | SX1276 | | ? + ?        || IO          || tbd (35-45)  || Arduino-IDE compatible     |
| Netblocks         | | SX1272 | | STM32L151    || IO          || 35,-         || program with ST-link       |
| Libelium          | | SX1272 | | -            || Bee         || 45,-         || Arduino library available  |
| HopeRF RFM92W     | | SX1272 | | no           || 2mm pin smd || 10,-         || Working with Arduino       |
| HopeRF RFM95W     | | SX1276 | | no           || 2mm pin smd || 10,-         || Working with Arduino       |
| [NiceRF LoRa1276](http://goo.gl/CqBBWU) | | SX1276 | | no           || smd         || 10,-         || Working with Arduino and RaspberryPi   |
| [Lora Shield V95](http://wiki.dragino.com/index.php?title=Lora_Shield)     | | SX1276 | | no           || Arduino Shield || 18,-         || HopeRF Module , Arduino Shield Style       |
| [Lora Shield V98](http://wiki.dragino.com/index.php?title=Lora_Shield)     | | SX1278 | | no           || Arduino Shield|| 18,-         || HopeRF Module, Arduino Shield Style       |
| Kerlink loramote  | | SX1272 | | yes          || IO          || 150,-        || professional; has GPS      |
| Embit EMB-LR1272  | | SX1272 | | yes          ||             || ?            ||                            |
| Froggyfactory     | | SX127X | | yes          || Uno         || 99,-         || This is LoRa FABian		|
| RFM95W + ESP8266  | | SX1276 | | esp8266      || DIY         || 10,-         || Arduino + [HLC](http://forum.thethingsnetwork.org/t/hoeks-ma-location-hlc-zonder-gps-dat-vreet-batterij/484)
| RFM95 + Arduino Pro Mini	|	| SX1276|| Atmega 28	|| DIY	|| 9,-	|| LMIC-1.51 library with smaller AES
| IMST iM880a       | | SX1272 | | STM32L151Cx  || smd         || 19.-         || program with ST-link       |
| Microchip RN2483  | | SX1276 | | yes PIC?     || smd         || 12.-         || +Lorawan stack, see [microchip](http://www.microchip.com/wwwproducts/Devices.aspx?product=RN2483) |
| Modtronix inAir9B | | SX1276 | | no           || 2.4mm       || 15.-         || Tested with Teensy 3.2 & LMIC 1.5 |

LoRa devices are roughly divided into two categories:

 1. Devices containing just the LoRa transceiver chip. These tranceivers are low-level devices that can transmit arbitrary data using the LoRa (and also FSK) modulation. They do not know anything about the LoRaWAN protocol and packet format, so they need an external microcontroller to implement the LoRaWAN stack.
 2. Full-stack LoRaWAN devices containing the transceiver and a microcontroller. The microcontroller typically implements the LoRaWAN stack and exposes a single TTL serial interface (using AT-commands) that can be used to control the module (similar to how XBee modules work) externally, though you can typically also integrate your own application into the same microcontroller.

Some devices are somewhat hybrid - they contain the transceiver and a microcontroller, but instead of supplying a full, precompiled LoRaWAN stack and exposing a serial API, they supply the code for the LoRaWAN stack so you can run both the LoRaWAN stack and your own application inside the microcontroller.

### DIY ESP8266 + Hopermf -> $10
Port of LMIC library to the ESP8266 based NodeMCU board and a DS18B20 temperature sensor (working).

* [https://github.com/things4u/LoRa-Thing/tree/master/esp-lmic-v1.5-ds18b20](https://github.com/things4u/LoRa-Thing/tree/master/esp-lmic-v1.5-ds18b20)

Documentation is on [http://things4u.github.com](http://things4u.github.com) 
the system is working on a Wemos D1-Mini NodeMCU-like board so will probably work 
with most other NodeMCU boards as well.

Other project of Hoeksma (Work in process)

* http://forum.thethingsnetwork.org/t/hoeks-ma-location-hlc-zonder-gps-dat-vreet-batterij/484



### RFM95 and Arduino Pro-Mini (Atmega 328) running full LMIC-1.5 stack with smaller AES encryption lib

As the LMIC-1.5 library does not fit for the Atmega 328 based MCU's, most importantly because the static AES datastructures in aes.cpp are very large,
another encryption library has been used in this LMIC version that uses far less memory.

It is possible to build very small and cheap sensors using for example the Arduino Pro-Mini ($1.50-$2.00 on Aliexpress) and a RFM95 module. 
Total cost would be less than 9 Euro. But of course it is also possible to use an Arduino Uno incombination with a shield and nice antenna.

You can find the code on [Things4U github](https://github.com/things4u/LoRa-LMIC-1.51). 
The documentation is on things4u.github.io
 
 

### SODAQ Mbili/Tatu with LoRaBee
The SODAQ Mbili and Tatu are based on the ATmega1284P and Arduino compatible. They do not do LoRaWAN by itself, but they contain a "Bee socket" and can be combined with the LoRaBee, which is a full-stack LoRaWAN board (based on the Embit EMB-LR1272 or Microchip RN2483) in Bee form factor.

Note that it should be possible to use the LoRaBee with other (Arduino) boards, using an XBee shield or breakout.

Get them:

* Tatu: [http://shop.sodaq.com/en/sodaq-tatu.html](http://shop.sodaq.com/en/sodaq-tatu.html)
  OR Mbili (bigger): [http://shop.sodaq.com/en/sodaq-mbili.html](http://shop.sodaq.com/en/sodaq-mbili.html)
* LoRa bee (based on EMB-lr1272): [http://shop.sodaq.com/en/lorabee.html](http://shop.sodaq.com/en/lorabee.html)
  OR LoRa bee based on RN2483: [http://shop.sodaq.com/en/lorabee-rn2483.html](http://shop.sodaq.com/en/lorabee-rn2483.html)

Program them:

1. Download the latest Arduino IDE: [https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software)
2. Install hardware support for Tatu: [https://github.com/SodaqMoja/HardwareTatu](https://github.com/SodaqMoja/HardwareTatu).
   Ignore the part on bootloaders, just extract the zip within the Arduino hardware folder and restart the IDE.
3. Install dependencies: [https://github.com/bblanchon/ArduinoJson](https://github.com/bblanchon/ArduinoJson)
4. Clone our demo repository: [https://github.com/TheThingsNetwork/loraduino](https://github.com/TheThingsNetwork/loraduino)
   Note: if you have the newer LoraBee based on the Microchip RN2483, you probably want to start from this library:
   [https://github.com/SodaqMoja/Sodaq_RN2483](https://github.com/SodaqMoja/Sodaq_RN2483).
   Please let us know if you made a nice example application repository.
5. Add sensors, add custom logic in the .ino Arduino sketch file:
    * uncomment the right `DEVICE_` line, optionally change other define statements on top
    * you may want to change the `measure()` and `send_measurement()` functions for your particular sensors
    (for help, read the [https://www.google.nl/search?q=arduino+getting+started+pdf](Arduino - Getting Started) book).
    * set a unique device ID in `EmbitBee.h` (search for `NETWORK_ADDRESS` and update `uint8_t Address[4]={0xAA, 0xFF, 0x01, 0x10};`).   
6. Compile, Upload, boot.
   The device will start sending measurements about once every two minutes.


### Kickstarter TTN Arduino UNO
We ran a Kickstarter campaign in 2015, including an Arduino UNO with built-in
LoRa chip and open-source libraries to connect to The Things Network gateways.
More info: [http://thethingsnetwork.org/landing/kickstarter](http://thethingsnetwork.org/landing/kickstarter)

This board will be an Arduino-compatible board with a full-stack [Microchip RN2483 Class A LoRaWAN module](http://www.microchip.com/wwwproducts/Devices.aspx?product=RN2483) integrated (so 2 microcontrollers on board - one in the LoRaWAN module and one on the main board for you to program), making it a perfect board to get started.
Early version of the docs (for beta testers) are available [here](http://forum.thethingsnetwork.org/t/ttn-uno-beta-release-documentation/290) (mirror [docs](https://www.dropbox.com/s/679gjqza5fk5tp3/LoRa%20QuickStart%20Guide%20%28English%29.pdf?dl=0) and [code](https://www.dropbox.com/s/vg53hw5plkjxi3h/LoRa_with_button_and_led_test_working.zip?dl=0)). Microchip's RN2483 LoRa Technology Module Command Reference User's Guide is [here](http://ww1.microchip.com/downloads/en/DeviceDoc/40001784C.pdf).

As we're getting closer to shipping this page will be updated with instructions.


### Netblocks
Netblocks offer a LoRa board containing a transceiver paired with an ARM processor. Netblocks supplies examples containing the Semtech LoRaWAN stack, that you can integrate with your own code to run on the single ARM processor.

We're working on support for the Netblocks, but not everything's working yet.

Get them:

* Choose one of the kits: [http://www.netblocks.eu/shop/](http://www.netblocks.eu/shop/)

Program them:

1. [https://github.com/TheThingsNetwork/XRange](https://github.com/TheThingsNetwork/XRange)
2. ask us what to do next ;-)

### IMST iM880a
This module has an SX1272 and a Cortex M3 MCU that you can also use to program directly. Toolchain is not as easy to use as Arduino (especially on non-Windows OSes). To program it, you can either get an ST-Link in-circuit debugger or use the starter kit board that IMST also sells.

### Libelium
Libelium has SX1272 modules that contain the Semtech SX1272 transceiver and an antenna plug. They use the Bee form factor, but do not use TTL serial like most Bee modules, but instead use SPI serial. If you use these modules, make sure to doublecheck the pinout, most XBee shields will likely not have the right connections.

I'm not sure about the status of the Libelium + TTN LoRaWAN, but there's people working on it.

Get them:

[https://www.cooking-hacks.com/shop/wireless/extreme-range-lora](https://www.cooking-hacks.com/shop/wireless/extreme-range-lora)
You'll need the Libelium LoRa Bee, and MCU (like Arduino or rPi) and a shield to connect the two.
There's also the [Waspmote platform](https://www.cooking-hacks.com/shop/waspmote/wireless/extreme-range-lora-sx1272-module-shield-waspmote), which according to their own website uses different Libelium LoRa Bees (incompatible with the Arduino/rPi version). It has [instructions on building a simple single-band gateway](http://www.libelium.com/downloads/documentation/waspmote_lora_868mhz_915mhz_sx1272_networking_guide.pdf). Note: this is not LoRaWAN.

### HopeRF

RFM92W and RFM95W (SX1272/SX1276). Can be ordered here: [http://www.hoperf.nl/LoRa](http://www.hoperf.nl/LoRa)

These are tiny boards that contain just a transceiver chip and some supporting components. These transceivers are just the SX1272 and SX1276 manufactured by Semtech, but rebranded by HopeRF.

Has been successfully tested on The Things Network using a Teensy and LMIC (see below)!

**How to build a Teensy TTN node!**

Cost: less than €30 (incl. VAT).

 * Use Teensy LC (or 3.1/3.2): [Teensy LC - Low Cost](https://www.pjrc.com/teensy/teensyLC.html)
 * Install Teensyduino, a software add-on for the Arduino: [Teensyduino](https://www.pjrc.com/teensy/teensyduino.html)
 * Buy the RFM92W or RFM95 (see above)
 * Clone [https://github.com/tftelkamp/arduino-lmic-v1.5](https://github.com/tftelkamp/arduino-lmic-v1.5)
 * Connect the RFM92/95 to the Teensy:
    * Teensy LC/3.1/3.2  -- RFM92/95 
    * GND -- GND
    * 3.3V -- 3.3V
    * 2 -- DIO0
    * 5 -- DIO1
    * 6 -- DIO2
    * 9 -- RESET
    * 10 -- NSS
    * 11 -- MOSI
    * 12 -- MISO
    * 13 -- SCK
 * Add a 1/4 wavelength antenna wire (+/- 8.2cm) on RFM92/95 ANA pin
 * Change the device addr (DevAddr) in the example, and compile/upload
 * Run, and check the TTN API!
 
 Notes:
 
 * The Teensy LC and 3.1 can support 100mA on the 3.3v pin, this is just enough for the RFM92/95 transmitting at 17dBm, but does not leave much room for other addons.
 * You can use different pins for the DIO 0/1/2 connections, but make sure to change the pin mappings in the example code as well
 * The library defaults to RFM92, change the radio type in config.h to use the RFM95
 * You can power the Teensy via the USB port, or a battery (e.g. 3.7V) on the 5v pin. But not both at the same time.
 * Questions? -> Forum!
 
### Modtronix inAir9B & Teensy 3.2
 * wired in the same manner as the Teensy & HopeRF above
 * Antenna: +2db antenna with male SMA connector
 * Tested with LMIC 1.5 and the example program
 
### Kerlink Loramote
This device should work out-of-the-box. It will start sending GPS, temperature and battery data as soon as it is powered.

TODO: custom applications compile. Kerlink has a nice wiki with instructions.


### MultiTech Systems mDot module
This module is available in surface mount or with xbee compatible pins.
The default firmware as shipped from the factory has an AT command interfacethat enables the mDot to be used with another mcu or USB to serial device.

For advanced users, the firmware can be replaced using the [mbed programming environment](https://developer.mbed.org/).
The mDot hardware is described at [https://developer.mbed.org/platforms/MTS-mDot-F411/](https://developer.mbed.org/platforms/MTS-mDot-F411/).
Programming requires the [mDot Developer Kit](http://www.multitech.com/models/94558010LF) although it is possible to upload firmware via the bootloader.

An example application that works with The Things Network is at [https://developer.mbed.org/users/SomeRandomBloke/code/mDot_TTN_DS18B20/](https://developer.mbed.org/users/SomeRandomBloke/code/mDot_TTN_DS18B20/).


### Dragino Lora Shield
Dragino Lora Shield is an easy to use Arduino Shield to test the Lora Technolog. it use the SX127x chip and compatible with both 3.3v/5v level Arduino board.  With the lora shield, User can test the TTN network just in few steps. A simpel demo set up can be found from [Instructable](http://www.instructables.com/id/Use-Lora-Shield-and-RPi-to-Build-a-LoRaWAN-Gateway/): It shows:

 * How to use Lora Shield to set up single channel gateway for TTN network.
 * How to use Lora Shield to set up a Lora Node.
 * How is the communication between the Lora Node and Lora Gateway.


### Do you know about other devices? Add them here!

## LoRaWAN stacks for transceiver-only devices
There are currently two open-source LoRaWAN stacks available for running LoRaWAN nodes:
 1. [IBM LMIC (LoraMac-in-C)](http://www.research.ibm.com/labs/zurich/ics/lrsc/lmic.html)
 2. [Semtech LoRaMac-node](https://github.com/Lora-net/LoRaMac-node)

Note that both say "LoRaMAC", which was the predecessor protocol to LoRaWAN. Semtech also has some code available to run on the gatweway side.

The LMIC code is being ported to the Arduino platform. A basic port (only works for node-to-node communication, no LoRaWAN support yet) is available by [Matthijs Kooijman](https://github.com/matthijskooijman/arduino-lmic) (check out the wiki on the repository too). Another version of this library is availble by [Thomas Telkamp](https://github.com/tftelkamp/arduino-lmic-v1.5), which uses the 1.5 verion of LMIC and has been succesfully tested with LoRaWAN and TTN already. The intention is to merge these two repositories together soon.

Both of the LMIC verions mentioned above currently run into memory limitations when running on a basic Arduino Uno (ATmega 328p). It turns out that most of the memory is taken up by AES constants, which can be moved from RAM into flash (not tried yet). Even then, a basic transmit example will still take up nearly all of the flash space on a 328p, so running LoRaWAN using LMIC on a 328p is probably not feasible without significant optimizations. The Semtech stack has not been ported to Arduino yet, perhaps it is more compact.

This LMIC Arduino library has been succesfully tested on a Teensy LC (ARM with sufficient memory). Work is ongoing to get it to work on an ATmega1284p board and the ESP2866 chip as well.

## General settings instructions
There are a couple of settings in LoRaWAN related to The Things Network
that all devices (no matter the LoRaWAN implementation) should set:

  * Network key / NwkSKey: a fixed network key for all The Things Network devices.
    It is `2B7E151628AED2A6ABF7158809CF4F3C` or in bytes (c++): `{0x2B, 0x7E, 0x15, 0x16, 0x28, 0xAE, 0xD2, 0xA6, 0xAB, 0xF7, 0x15, 0x88, 0x09, 0xCF, 0x4F, 0x3C}`.
    This key is used for calculating message integrity (MIC). It is only used for payload encryption if Port = 0 (MAC commands, not yet implemented in The Things Network).
  * Application session key / AppSKey: used for encryption of the payload (Port > 0). To get started, use the default one,
    which is identical to the Network key (note this will make all your testdata publicly available through our API).
  * DeviceID / Device Address: this should be unique per node.
    In the final routing implementation we expect to have blocks of devices
    being routed to application servers. But for now, you can pick anything
    you like; after testing, be sure to [Register your address space here](../AddressSpace).
  * Application key / AppKey: a key specific for an application. Used for over-the-air activation, not yet implemented in The Things Network.
  * Frequencies: The Kerlink gateways are listening to all SF on 868.1, 868.3, 868.5, 867.1, 867.3, 867.5, 867.7, 867.9 Mhz, SF7/250Khz on 868.3 MHz, and FSK (50kbps) on 868.8 MHz. See: [LoRaWAN Frequencies](http://thethingsnetwork.org/wiki/LoRaWAN-Frequencies)


# Software (where's my data?)
[Software Overview](http://thethingsnetwork.org/wiki/Software/Overview)


**[back to GettingStarted](../GettingStarted)**