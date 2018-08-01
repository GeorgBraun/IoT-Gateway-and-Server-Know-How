# BLE, Bluetooth Low Energy

## High-level introductions

#### Kelvin Aviles: Bluetooth Low Energy App Development: An Intro

* https://www.youtube.com/watch?v=Y2cEbZw_R6M
* 4 minutes
* Really short intro, basically just difference between Bluetooth and Bluetooth Low Energy and what beacons are used for


#### Adafruit Industries, Collin's Lab - Bluetooth Low Energy

* https://www.youtube.com/watch?v=ItV08vGqACM
* 5 minutes
* Short, high level intro to what BLE is used for 

**Contents:**
1. Mentions the "Bluefruit LE Connect" app
2. Application examples with Adruino (no technical details)
3. Beakon


## More technical details

#### Kelvin Aviles: Bluetooth Low Energy App Development: The Basics
* https://www.youtube.com/watch?v=MzM3-YWftxE
* 6 minutes
* Short and vary helpful!

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

   

#### Nordic Semiconductor: Intro to Bluetooth low energy and BLE development with Nordic Semiconductor

* https://www.youtube.com/watch?v=pLgnHuGI69s
* 27 minutes
* Similar to Kelvin Aviles' videos above, but slower and a bit more details

**Contents:**
1. Device roles: Broadcaster, Observer, Peripheral Central
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

