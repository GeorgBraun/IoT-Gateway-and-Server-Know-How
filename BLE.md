﻿# BLE, Bluetooth Low Energy

**Contents of this page**

<!-- TOC depthFrom:2 depthTo:4 -->

- [High-level Introductions](#high-level-introductions)
    - [1. Kelvin Aviles: Bluetooth Low Energy App Development: An Intro](#1-kelvin-aviles-bluetooth-low-energy-app-development-an-intro)
    - [2. Adafruit Industries, Collin's Lab - Bluetooth Low Energy](#2-adafruit-industries-collins-lab---bluetooth-low-energy)
- [Technical Details](#technical-details)
    - [1. Kelvin Aviles: Bluetooth Low Energy App Development: The Basics](#1-kelvin-aviles-bluetooth-low-energy-app-development-the-basics)
    - [2. Nordic Semiconductor: Intro to Bluetooth low energy and BLE development with Nordic Semiconductor](#2-nordic-semiconductor-intro-to-bluetooth-low-energy-and-ble-development-with-nordic-semiconductor)
    - [3. Argenox Technologies: Introduction to Bluetooth Low Energy (BLE) v4.0](#3-argenox-technologies-introduction-to-bluetooth-low-energy-ble-v40)
    - [4. Argenox Technologies: A BLE Advertising Primer](#4-argenox-technologies-a-ble-advertising-primer)
    - [5. Wendy Warne: Bluetooth Low Energy - It starts with Advertising](#5-wendy-warne-bluetooth-low-energy---it-starts-with-advertising)
- [Implementations](#implementations)
  - [BLE Peripherals](#ble-peripherals)
    - [BBC micro:bit](#bbc-microbit)
    - [ESP32](#esp32)
  - [BLE Centrals](#ble-centrals)
    - [NodeJS and Noble](#nodejs-and-noble)

<!-- /TOC -->

<hr>

&nbsp;


## High-level Introductions

#### 1. Kelvin Aviles: Bluetooth Low Energy App Development: An Intro

* https://www.youtube.com/watch?v=Y2cEbZw_R6M
* 4 minutes
* Really short intro, basically just difference between Bluetooth and Bluetooth Low Energy and what beacons are used for

&nbsp;

#### 2. Adafruit Industries, Collin's Lab - Bluetooth Low Energy

* https://www.youtube.com/watch?v=ItV08vGqACM
* 5 minutes
* Short, high level intro to what BLE is used for 

**Contents:**
1. Mentions the "Bluefruit LE Connect" app
2. Application examples with Adruino (no technical details)
3. Beakon

&nbsp;


## Technical Details

#### 1. Kelvin Aviles: Bluetooth Low Energy App Development: The Basics
* https://www.youtube.com/watch?v=MzM3-YWftxE
* 6 minutes
* Short and very helpful!

**Contents:**
1. Peripherals and Centrals
2. GAP (Generic Access Protocol): Used by peripherals
3. GATT (Generic Attribute Profile): Used for communication between devices; hierarchical arrangement: Profiles -> Services -> Characteristics
4. Characteristics can read, write, notify
5. Connections
   * A Peripheral can only be connected to one Central. Once connected, a Peripheral will stop advertising.
   * A Central can be connected to many Peripherals at the same time.
6. UUIDs (Universally Unique Identifiers) are used for Devices, Profiles, Services, and Characteristics
   * 16-bit wide: Stanardized by SIG
     * List of Companies is at https://www.bluetooth.com/specifications/assigned-numbers/company-identifiers
     * List of Services is at https://www.bluetooth.com/specifications/gatt/services
     * List of Characteristics ist at https://www.bluetooth.com/specifications/gatt/characteristics
   * 128-bit wide: custom, user specific

&nbsp;


#### 2. Nordic Semiconductor: Intro to Bluetooth low energy and BLE development with Nordic Semiconductor

* https://www.youtube.com/watch?v=pLgnHuGI69s
* 27 minutes
* Similar to Kelvin Aviles' videos above, but slower and a bit more details

**Contents:**
1. Device roles: Broadcaster, Observer, Peripheral, Central
2. Advertising channels
3. Identifying devices: MAC addresses
4. Identifying applications (also known as "profiles"): Universal Unique Identifiers (UUIDs)
   * 16-bit for applications defined by SIG (e.g. 0x180D for heart rate, 0x180F for battery service, 0x180A for device information)
   * 128-bit for custom applications
5. Initiate and establish a connection
6. Profile (application), Service (functionality of application), Characteristic (performs a functionality of its service)
   * Services and characteristics are declared by their UUID
7. CCCD (Client Characteristic Configuration Descriptor) can be used to enable/disable notifications
8. Typical scenario:
   * The Peripheral device is the server, offering some data (e.g. heart rate sensor)
   * The Central device is the client, receiving/consuming the data (e.g. cell phone)
9. Basic information about the nRF52 chips from Nordic

&nbsp;


#### 3. Argenox Technologies: Introduction to Bluetooth Low Energy (BLE) v4.0

* http://www.argenox.com/bluetooth-low-energy-ble-v4-0-development/library/introduction-to-bluetooth-low-energy-v4-0/
* Short, high-level, nice

&nbsp;


#### 4. Argenox Technologies: A BLE Advertising Primer

* http://www.argenox.com/bluetooth-low-energy-ble-v4-0-development/library/a-ble-advertising-primer/
* In-depth, very helpful explanation about BLE Advertising protocol and data packets
* Includes "A Quick Look into UUIDs" with the standard 12 byte wide UUID base for 16 byte wide UUIDs `XXXXXXXX-0000-1000-8000-00805F9B34FB`.
  * The leading 4 bytes are standardized by the bluetooth spec. If only 2 bytes are used, the remaining leading 2 bytes are 0.
  * For example, the "Battery Service" is assigned to the 2 byte ID `0x180F` (see https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.service.battery_service.xml)<br>
    The corresponding full blown 16 byte UUID is then `0000180f-0000-1000-8000-00805f9b34fb`
  * This also means: self created UUIDs **must not** follow the `XXXXXXXX-0000-1000-8000-00805F9B34FB` pattern since this is reserved for standardized UUIDs.
* Also includes "BLE Beacons and iBeacons"

&nbsp;


#### 5. Wendy Warne: Bluetooth Low Energy - It starts with Advertising

* https://blog.bluetooth.com/bluetooth-low-energy-it-starts-with-advertising?_ga=2.16106166.140214492.1536600728-1140941370.1536600728
* Short, technical introduction about advertising data packet

&nbsp;


## Implementations

### BLE Peripherals

#### BBC micro:bit

The BBC micro:bit (https://en.wikipedia.org/wiki/Micro_Bit and https://microbit.org/) is a single board embedded system including 
* a micro controller (Nordic nRF51 comprising an ARM Cortex-M0)
* a 3-axis accelerometer
* a 3-axis magnetometer
* an LED matrix
* a micro-USB-connector
* a Bluetooth low energy 4.1 interface

The BBC micro:bit can be programmed with many different programming languages using graphical programming as well as traditional text based IDEs, like the Arduino IDE.

One excellent tutorial is provided by  Limor Fried (aka _"Lady Ada"_) from Adafruit Industries: "Micro:bit with Arduino" on https://learn.adafruit.com/use-micro-bit-with-arduino?view=all (or as PDF on https://cdn-learn.adafruit.com/downloads/pdf/use-micro-bit-with-arduino.pdf).

After the tutorial, you are able to read one of the micro:bits sensors (e.g. the accelerometer), transmit the values to a paired cell phone via BLE and display it with the free app "Adafruit Bluefruit LE Connect".



#### ESP32

details to come ...

&nbsp;


### BLE Centrals

Important hint:

On Linux including Raspbian, you usually have to act as root (e.g. via `sudo`) to access Bluetooth and BLE devices. This can be avoided by adding Bluetooth permissions to the tools and server apps, that you want to use with Bluetooth. As described on https://github.com/mozilla-iot/gateway/blob/master/README.md#set-up-bluetooth-permissions and on https://github.com/noble/noble#running-without-rootsudo this can be done as follows:

```bash
# For NodeJS:
sudo setcap cap_net_raw+eip $(eval readlink -f `which node`)

# For Python 3:
sudo setcap cap_net_raw+eip $(eval readlink -f `which python3`)
```

In case there is no `setcap` command on your system, you can install it by `sudo apt-get install libcap2-bin`.

#### NodeJS and Noble

To program a BLE central in NodeJS, use Noble from https://github.com/noble/noble. While the GitHub-Page provides an overview about scanning, connecting, ... you probably need a little tutorial. For example, you may take a look at Nic Raboy's tutorial "Use Node.js And A Raspberry Pi Zero W To Scan For BLE iBeacon Devices" from 2018 at https://www.youtube.com/watch?v=AFjYKEf7j2M. Hint: Instead of developing the initial project on your Mac or PC, you may just as well start directoly on the RPi. The newer models are fast enough for this.
