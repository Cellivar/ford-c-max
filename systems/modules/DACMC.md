# Digital Audio Control Module C

| Module Property     | Value           | Notes |
| ------------------- | --------------- | ----- |
| AsBuilt Module Code | 7D5             |       |
| Part number         | DM5T-14F509-AG  |       |
| Calibration         |                 |       |
| Strategy            | DP5T-14F539-AJ  |       |
| Calibration Level   | DM5T-14F509-AG  |       |
| Location            | Behind glovebox |       |
| Bus                 | MS-CAN          |       |

The DACMC is a combination audio amplifier and audio effect generator. On C-Max vehicles this is used as an amp for the various speakers and is also used as the Active Noise Cancellation system controller.

In a Mustang the DACMC is used for the fake engine vroom noise!

The DACMC and its three microphone system is the subject of [TSB 14-0151 POWERTRAIN DRONING NOISE](/maintenance/tsbs/README.md), though the root cause is the microphones that go into the DACMC.

If you want to _disable_ ANC that control is in the [ACM](./ACM.md) module, for some reason the module that actually does the ANC doesn't control whether it should be doing the ANC.

The DACMC has an internal audio EQ system that can be configured with FORScan. My ears are not good enough to tell what the difference is so I left it on default (01) after playing around.

## AsBuilt Configuration

| 07D5-01-01 | Nibble (hex) | Bit | Effect                                  | Notes  |
| ---------- | ------------ | --- | --------------------------------------- | ------ |
|            | 0            | 0   | Front amp/speaker type                  | Note 1 |
|            |              | 0   | Front amp/speaker type                  |        |
|            |              | 1   | Rear amp/speaker type                   | Note 1 |
|            |              | 0   | Rear amp/speaker type                   |        |
|            | 0            | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            | 2            | 0   | Disable front speaker detection         |        |
|            |              | 0   | Disable rear speaker detection          |        |
|            |              | 1   | Disable chimes diagnostics              |        |
|            |              | 0   |                                         |        |
|            | 8            | 1   | Missing message strategy - architecture | Note 2 |
|            |              | 0   | Missing message strategy - D385         | Note 2 |
|            |              | 0   |                                         |        |
|            |              | 0   |                                         |        |
|            |              | -   |                                         |        |
|            | 0            | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            | 0            | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
|            |              | 0   | (Reserved)                              |        |
| CHECKSUM   | 06           |     | Autocalculated                          |        |
|            |              |     |                                         |        |
| 07D5-02-01 | Nibble (hex) | Bit | Effect                                  | Notes  |
|            | 0            | 0   | EQ Selection                            | Note 3 |
|            |              | 0   | EQ Selection                            |        |
|            |              | 0   | EQ Selection                            |        |
|            |              | 0   | EQ Selection                            |        |
|            | 1            | 0   | EQ Selection                            |        |
|            |              | 0   | EQ Selection                            |        |
|            |              | 0   | EQ Selection                            |        |
|            |              | 1   | EQ Selection                            |        |
| CHECKSUM   | E0           |     | Autocalculated                          |        |

### Note 1: Front/rear speaker type

2 bits each to determine what the DACMC is driving on its speaker output wires.

* 00: Internal amp (C-Max default for both)
* 01: External variable amp
* 10: External line-level amp
* 11: Not used

### Note 2: Missing message strategy

It's not clear what 'missing message' strategy means nor what D385 means, but these are the values. C-Max is I-CAN based.

* Architecture
  * 0: CGEA 1.3
  * 1: Non-CGEA 1.3 (C-Max Default)
* D385
  * 0: Non-D385 (C-Max Default)
  * 1: D385

### Note 3: EQ Selection

This sets the EQ levels the DACMC uses internally. The two nibbles are used together as a lookup table, so this is a list of bytes.

My ears couldn't tell much of a difference but I didn't spend much time playing around here. Apparently these are vehicle specific.

* 00: "Flat"
* 01: Unknown (C-Max Default, including Premium Audio)
* 02: Unknown
* 03: Unknown
* 04: Unknown
* 05: Unknown
* 06: Unknown
* 07: Unknown
* 08: Unknown
* 09: Unknown
* 0A-0F: Reserved

## Sources

* [Cyanlabs](https://cyanlabs.net/asbuilt-db/dacmc-2013-2018-asbuilt-database/)
