# Audio Control Module

| Module Property     | Value                     | Notes |
| ------------------- | ------------------------- | ----- |
| AsBuilt Module Code | 727                       |       |
| Part number         | CM5T-19C107-LA            |       |
| Calibration         | CM5T-14D100-LA            |       |
| Strategy            | CM5T-14D099-FD            |       |
| Calibration Level   | CM5T-19C107-LA            |       |
| Location            | Behind APIM, with CD slot |       |
| Bus                 | MS-CAN                    |       |

## AsBuilt Configuration

| 0727-01-01 | Nibble (hex) | Bit | Effect                                | Notes                                        |
| ---------- | ------------ | --- | ------------------------------------- | -------------------------------------------- |
|            | 1            | 0   | Enable internal Sat Radio service     | SiriusXM is referred to as SDARS here        |
|            |              | 0   | APIM Type                             | 0 = Gen 2, 1 = Gen 1                         |
|            |              | 0   | Electronic Feature Panel Interface    | 0 = CAN (C-Max), 1 = LIN                     |
|            |              | 1   | Enable APIM Available                 |                                              |
|            | 8            | 1   | Enable HD Radio                       |                                              |
|            |              | 0   | Enable DAB Tuner                      | EU-only feature                              |
|            |              | 0   | Enable CAN steering wheel controls    | C-Max buttons aren't CAN                     |
|            |              | 0   | Enable Shaker System                  | Mustang thing?                               |
|            | 5            | 0   | Front amp/speaker type                | Note 1                                       |
|            |              | 1   | Front amp/speaker type                | Note 1                                       |
|            |              | 0   | Rear amp/speaker type                 | Note 1                                       |
|            |              | 1   | Rear amp/speaker type                 | Note 1                                       |
|            | 0            | 0   | Aux 1 output                          | Note 2                                       |
|            |              | 0   | Aux 1 output                          | Note 2                                       |
|            |              | 0   | Aux 2 output                          | Note 2                                       |
|            |              | 0   | Aux 2 output                          | Note 2                                       |
|            | F            | 1   | Disable front speaker detection       |                                              |
|            |              | 1   | Disable rear speaker detection        |                                              |
|            |              | 1   | Enable active antenna                 | 0 = "Mast", 1 = "Active" (C-Max)             |
|            |              | 1   | Number of presets                     | 0 = 10 presets, 1 = 6 presets                |
|            | E            | 1   | Enable front tweeters                 | They're up by the windshield                 |
|            |              | 1   | Chime strategy                        | 0 = CGEA, 1 = C1MCA                          |
|            |              | 1   | Enable ANC                            | See [manual method](/projects/remove_anc.md) |
|            |              | 0   | Enable USB                            |                                              |
|            | 0            | 0   | Aux 1 out location                    | Note 2                                       |
|            |              | 0   | Aux 1 out location                    | Note 2                                       |
|            |              | 0   | Aux 1 out location                    | Note 2                                       |
|            |              | 0   | Aux 2 out location                    | Note 2                                       |
|            | 0            | 0   | Aux 2 out location                    | Note 2                                       |
|            |              | 0   | Aux 2 out location                    | Note 2                                       |
|            |              | 0   | Internal / External CD Mode           | 0 = Internal, 1 = External/No CD             |
|            |              | 0   | Enable MP3 CD Text Conversion         |                                              |
|            | 0            | 0   | Disable center channel open detection |                                              |
|            |              | 0   | Enable Aux Audio Module (AAM)         |                                              |
|            |              | 0   | Enable Convertible vehicle            | Also 0 on pano sunroof                       |
|            |              | 0   | Enable turn signal chimes             | IPC handles these                            |
|            | 0            | 0   | Enable Demand Lamp                    | ???                                          |
|            |              | 0   |                                       |                                              |
|            |              | 0   | Enable tune knob acceleration         |                                              |
|            |              | 0   |                                       |                                              |
| CHECKSUM   | 96           |     | Autocalculated                        |                                              |

| 0727-01-02 | Nibble (hex) | Bit | Effect         | Notes  |
| ---------- | ------------ | --- | -------------- | ------ |
|            | 0            | 0   | EQ Selection   | Note 3 |
|            |              | 0   |                |        |
|            |              | 0   |                |        |
|            |              | 0   |                |        |
|            | 0            | 0   |                |        |
|            |              | 0   |                |        |
|            |              | 0   |                |        |
|            |              | 0   |                |        |
| CHECKSUM   | 2A           |     | Autocalculated |        |

| 0727-02-01 | Nibble (hex) | Bit | Effect                  | Notes  |
| ---------- | ------------ | --- | ----------------------- | ------ |
|            | 0            | 0   | AM Antenna test station | Note 4 |
|            |              | 0   |                         |        |
|            |              | 0   |                         |        |
|            |              | 0   |                         |        |
|            | 0            | 0   |                         |        |
|            |              | 0   |                         |        |
|            |              | 0   |                         |        |
|            |              | 0   |                         |        |
| CHECKSUM   | 2A           |     | Autocalculated          |        |

| 0727-03-01 | Nibble (hex) | Bit | Effect                      | Notes  |
| ---------- | ------------ | --- | --------------------------- | ------ |
|            | 0            | 0   | AM Acceptable test strength | Note 4 |
|            |              | 0   |                             |        |
|            |              | 0   |                             |        |
|            |              | 0   |                             |        |
|            | 0            | 0   |                             |        |
|            |              | 0   |                             |        |
|            |              | 0   |                             |        |
|            |              | 0   |                             |        |
| CHECKSUM   | 2A           |     | Autocalculated              |        |

| 0727-04-01 | Nibble (hex) | Bit | Effect             | Notes                                                 |
| ---------- | ------------ | --- | ------------------ | ----------------------------------------------------- |
|            | 0            | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            | 0            | 0   | Tuner Region       | Note 5                                                |
|            |              | 0   | Tuner Region       |                                                       |
|            |              | 0   | Tuner Region       |                                                       |
|            |              | 0   | Tuner Region       |                                                       |
|            | 0            | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            | 0            | 0   | SDARS Region       | Note 6                                                |
|            |              | 0   | SDARS Region       |                                                       |
|            |              | 0   | SDARS Region       |                                                       |
|            |              | 0   | SDARS Region       |                                                       |
|            | 0            | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            |              | 0   |                    |                                                       |
|            | 0            | 0   | SDARS Data Service | Note 6                                                |
|            |              | 0   | SDARS Data Service |                                                       |
|            |              | 0   | SDARS Data Service |                                                       |
|            |              | 0   | SDARS Data Service |                                                       |
|            | 0            | 0   | Country Code       | [Country Code](/systems/modules/ford_country_code.md) |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            | 0            | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            | 0            | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            | 0            | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
|            |              | 0   | Country Code       |                                                       |
| CHECKSUM   | 2A           |     | Autocalculated     |                                                       |

The other blocks are where radio presets are stored. I speculate this is so Ford IDS can back up and restore the presets for procedures that involve messing with the ACM.

* 0727-05-01 thru 02: AM Presets
* 0727-06-01 thru 04: FM Presets
* 0727-07-01 thru 04: FM Presets
* 0727-08-01 thru 06: SirisXM/HD Radio/DAB Presets

### Note 1: Amp / Speaker Type

This controls how the internal ACM amp should attempt to power the speaker output channels.

* 00 = Internal ACM amp
* 01 = External variable amp (C-Max Default)
* 10 = External line-level amp
* 11 = Not used

C-Maxes use an external variable amp, where 4V is the Vref1 value.

Line level is sometimes referred to as 'smart amp'.

### Note 2: Aux outputs and location

There are 2 aux outputs from the ACM that can be configured independently to drive additional speakers or subs.

* 00 = Not used (C-Max Default)
* 01 = Internal ACM amp
* 10 = External sub
* 11 = External speaker

The Sony sound system uses Aux 2 set to internal amp (01).

Speakers and subs are Vref 1-4 volts.

The Sync interface lets you control balance and fade settings, so the ACM can be configured with where in the vehicle the aux output is being routed to. This lets additional features play nice with the balance and fade settings in the UI.

* 000 = Mono sub
* 001 = Left front
* 010 = Center front
* 011 = Right front
* 100 = Right rear
* 101 = Center rear
* 110 = Left rear
* 111 = Left sub

Sony uses Aux 2 set to 010 (Center front)

### Note 3: EQ Selection

Other than the 'flat' EQ setting, the rest of these settings are not documented.

C-Maxes default to EQ 04.

* 00 = Flat
* 01 = Mode 01
* 02 = Mode 02
* etc..

### Note 4: AM Antenna Test

The ACM will self-test the AM tuning feature. You can set the station and expected dbuV value.

The station setting is in kHz, and the default is 46kHz (`2E`). At least according to the docs it is, but really 46kHz is not a real AM radio band, so something is amiss here.

The test signal strength defaults to `30`.

### Note 5: Tuner Region

Lookup table

* 0 = North America
* 1 = Global Car ("Rest of World")
* 2 = Japan
* 3 = Europe
* 4 = Asia/Pacific

### Note 6: SDARS Region

The region code is also a lookup table

* 0 = Unconfirmed
* 1 = USA
* 2 = Canada
* 3 = No Content

And the data service determines if Travel Link is enabled

* 0 = Unconfirmed
* 1 = Data Services Enabled
* 2 = No data services
