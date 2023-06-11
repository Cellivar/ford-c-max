# Telematics Control Unit - 3G Modem

| Module Property     | Value                        | Notes |
| ------------------- | ---------------------------- | ----- |
| AsBuilt Module Code | 754                          |       |
| Part number         | HJ5T-14G087-UM               |       |
| Calibration         |                              |       |
| Strategy            | HJ5T-14G139-UM               |       |
| Calibration Level   | HJ5T-14G087-UM               |       |
| Location            | Driver's side panel in trunk |       |
| Bus                 |                              |       |

As a result of the shutdown of 3G cell networks in the US and Canada these modules are no longer useful. Either you've upgraded to the 4G kit already, should _really_ do it as soon as possible before they shut down the program, or get to figure out how to retrofit a new 4G TCU yourself. Good luck.

## AsBuilt Configuration

The AsBuilt here is lengthy so is broken into sections.

### Communication block

The first two blocks concern feature support and communication type.

| 0754-01-01 | Nibble (hex) | Bit | Effect                               | Notes  |
| ---------- | ------------ | --- | ------------------------------------ | ------ |
|            | B            | 1   | Enable RF Section (RFSE)             | ???    |
|            |              | 0   | APIM Type                            | Note 1 |
|            |              | 1   | APIM Type                            |        |
|            |              | 1   | APIM Type                            |        |
|            | 8            | 1   | Engine type                          | Note 2 |
|            |              | 0   | Engine type                          |        |
|            |              | 0   | Engine type                          |        |
|            |              | 0   | Engine type                          |        |
|            | 4            | 0   | Vehicle Architecture                 | Note 3 |
|            |              | 1   | Vehicle Architecture                 |        |
|            |              | 0   | Vehicle Architecture                 |        |
|            |              | 0   |                                      |        |
|            | 2            | 0   | TCU Region                           | Note 4 |
|            |              | 0   | TCU Region                           |        |
|            |              | 1   | TCU Region                           |        |
|            |              | 0   | Disable Optional Configuration State | ???    |
| CHECKSUM   | 57           |     | Autocalculated                       |        |

| 0754-02-01 | Nibble (hex) | Bit | Effect                                      | Notes                            |
| ---------- | ------------ | --- | ------------------------------------------- | -------------------------------- |
|            | 1            | 0   |                                             |                                  |
|            |              | 0   |                                             |                                  |
|            |              | 0   | Enable On Line Telematics (OLT)             |                                  |
|            |              | 1   | Enable Customer Connectivity Settings (CCS) |                                  |
|            | E            | 1   | Enable data usage feature                   |                                  |
|            |              | 1   | Enable HEV/PHEV data monitoring             |                                  |
|            |              | 1   | Enable vehicle health monitor               |                                  |
|            |              | 0   | Enable Wi-Fi Hotspot                        | Requires specific TCU to support |
|            | A            | 1   | Enable Ford OTA                             |                                  |
|            |              | 0   | Enable PwPck Setting                        | Unclear effect                   |
|            |              | 1   | Enable transmission of rolling code         | Unclear effect                   |
|            |              | 0   | Enable secondary battery                    |                                  |
|            | 0            | 0   | Enable primary battery                      |                                  |
|            |              | 0   | Enable ECALL                                |                                  |
|            |              | 0   | Enable Tracking and Blocking Module         |                                  |
|            |              | 0   | Enable Crew Chief                           | Ford Pro feature?                |
| CHECKSUM   | 2A           |     | Autocalculated                              |                                  |

#### Note 1: APIM Type

This seems to influence how the TCU communicates to the APIM.

* 000 = Not configured
* 001 = Sync 1 (4" screen)
* 010 = Sync 2
* 011 = Sync 3
* 100 = No APIM Present

#### Note 2: Engine Type

* 1 = Gas
* 2 = Diesel
* 3 = FHEV
* 4 = Hydrogen Fuel Cell
* 5 = Diesel/Electric Hybrid (!?)
* 6 = CNG
* 7 = BEV
* 8 = PHEV
* 9-F = Reserved

#### Note 3: Vehicle Architecture

Set appropriately otherwise the MFM/Ford Pass things like lock/unlock and remote start will fail.

* 000 = Not configured
* 001 = CGEA 1.1
* 010 = CGEA 1.2 (C-Max Default)
* 011 = CGEA 1.3
* 100 = C1MCA (Doesn't work for C-Maxes!)
* 101 = Transit Connect (TCA)

### Note 4: TCU Destination Region

Likely controls the cell radio bands the TCU tries to use.

* 000 = Not configured
* 001 = North America
* 010 = Russia
* 011 = China
* 100 = EU
* 101 = South America
* 110 = Australia

### Alerts blocks

TCUs have many blocks of alert configurations. An alert takes up 1 byte and all alerts have the same meaning to the bits within the alert. I've not found solid information on any of the bits other than the lowest bit: enabled/disabled.

The first alert byte is described below, otherwise the list of alerts will be grouped by the block for brevity.

Generally speaking you'll want the alert byte to be either `7C` for disabled or `7D` for enabled. Just because an alert is enabled doesn't mean you'll see something in the app, several alerts are just for communication with Ford's servers.

| 0754-03-01 | Nibble (hex) | Bit | Effect                        | Notes                         |
| ---------- | ------------ | --- | ----------------------------- | ----------------------------- |
|            | 7            | 0   | QOS level?                    | Firmware upgrade status alert |
|            |              | 1   | QOS level?                    |                               |
|            |              | 1   | Alert send delay?             |                               |
|            |              | 1   | DRX continues?                |                               |
|            | D            | 1   | Connection time extension?    |                               |
|            |              | 1   | Connection time extension?    |                               |
|            |              | 0   | Disable alert in roaming?     |                               |
|            |              | 1   | Enable alert?                 |                               |
|            | 7            | 0   | Low 12V Battery Alert         |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            | D            | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 0   |                               |                               |
|            |              | 1   |                               |                               |
|            | 7            | 0   | Low 12V Battery Alert Clear   |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            | D            | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 0   |                               |                               |
|            |              | 1   |                               |                               |
|            | 7            | 0   | Low Tire Pressure Alert       |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            | D            | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 0   |                               |                               |
|            |              | 1   |                               |                               |
|            | 7            | 0   | Low Tire Pressure Alert Clear |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            | D            | 1   |                               |                               |
|            |              | 1   |                               |                               |
|            |              | 0   |                               |                               |
|            |              | 1   |                               |                               |
| CHECKSUM   | 2A           |     | Autocalculated                |                               |

* 0754-03-02
  * Master Reset Alert
  * TCU Connection Status Alert
  * Charge System Fault Alert
  * Plug Status Change Alert
  * Battery Performance Alert Clear
* 0754-03-03
  * Gear In Park Alert
  * Gear Out Of Park Alert
  * Battery Charge State Change Alert
  * Battery Performance Alert
  * Driver Conditioning Sync Alert
* 0754-03-04
  * Customer Requested SOC Reached Alert
  * Scheduler Drive Conditioning Sync Alert
  * Favorite Location Data Sync Alert
  * Charge SChedule Status Change Sync Alert
  * Scheduled Charge Not Occurring Alert
* 0754-03-05
  * Charged And Drive Condition Complete Alert
  * Vehicle Diagnostic Data Response Alert
  * Method 2 Config Change Response Alert
  * HEV Battery Fault Alert Clear
  * HEV Data Monitoring Alert
* 0754-03-06
  * HEV Data Monitoring Alert Publishing Frequency (First two bytes, see note 1)
  * User Authorization Response Alert
  * Provisioning Alert
  * Sleep State Change Alert
* 0754-03-07
  * Vehicle Alarm Triggered Alert
  * Motive Mode Begin Alert
  * Motive Mode End Alert
  * Remote Start End Alert
  * Remote Start Begin Alert
* 0754-03-08
  * Vehicle Health Data Alert
  * Low Fuel Alert

#### Note 1: HEV Data Publishing Interval

This two-byte field encodes the number of minutes between _pushes_ of EV charging data. The lower this number the more 12V battery the system will drain, but the faster you'll see updates in the app without having to manually refresh.

The value is the decimal number of minutes encoded as hex values. So:

0078 = 120 minutes
003C = 60 minutes
00E1 = 30 minutes

### Connection Configuration Blocks

The last two blocks are related to the cell power connection and timeout.

| 0754-05-01 | Nibble (hex) | Bit | Effect              |
| ---------- | ------------ | --- | ------------------- |
|            | 0            | 0   | Keep alive interval |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 0            | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 0            | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 0            | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 0            | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 0            | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 7            | 0   |                     |
|            |              | 1   |                     |
|            |              | 1   |                     |
|            |              | 1   |                     |
|            | 8            | 1   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            | 1            | 0   | Connection timeout  |
|            |              | 0   |                     |
|            |              | 0   |                     |
|            |              | 1   |                     |
|            | E            | 1   |                     |
|            |              | 1   |                     |
|            |              | 1   |                     |
|            |              | 0   |                     |
| CHECKSUM   | 2A           |     | Autocalculated      |

| 0754-05-02 | Nibble (hex) | Bit | Effect           |
| ---------- | ------------ | --- | ---------------- |
|            | 0            | 0   | Retry count      |
|            |              | 0   |                  |
|            |              | 0   |                  |
|            |              | 0   |                  |
|            | 2            | 0   |                  |
|            |              | 0   |                  |
|            |              | 1   |                  |
|            |              | 0   |                  |
|            | 7            | 0   | Keep alive timer |
|            |              | 1   |                  |
|            |              | 1   |                  |
|            |              | 1   |                  |
|            | 7            | 0   |                  |
|            |              | 1   |                  |
|            |              | 1   |                  |
|            |              | 1   |                  |
| CHECKSUM   | 2A           |     | Autocalculated   |

## Source

* [CyanLabs Database](https://cyanlabs.net/asbuilt-db/tcu-h-database/)
