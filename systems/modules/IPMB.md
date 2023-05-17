# Image Processing Module - B (Rear)

| Module Property     | Value                                               | Notes |
| ------------------- | --------------------------------------------------- | ----- |
| AsBuilt Module Code | 7B1                                                 |       |
| Part number         | CM5T-19H423-AB                                      |       |
| Calibration         | CM5T-14F018-AA                                      |       |
| Strategy            | CM5T-14F017-AB                                      |       |
| Calibration Level   | CM5T-19H423-AB                                      |       |
| Location            | Passenger side of trunk, behind seat belt retractor |       |
| Bus                 | MS-CAN                                              |       |

The IPMB is sometimes referred to as the "Parking Aid Camera Module" in some Ford documentation. My 2013 wiring diagram manual uses PACM instead of IPMB.

The IPMB serves mostly as a camera controller module, translating CAN bus commands to LIN bus commands to drive the camera itself. The camera has onboard smarts to draw things like the on-screen steering lines, the IPMB tells it what to draw.

The IPMB is only present on 2013-2015 C-Maxes. After the Sync3 switch the LIN bus was added directly to the Body Control Module and the IPMB functionality was integrated into it. I suspect most of these configuration elements moved to the 2016+ Body Control Module configuration, I've never had a newer vehicle to mess around with and find out.

My C-Max did not come with a factory rear view camera. I purchased the parts, added the wiring, and programmed the whole setup to work. [Read that writeup here](/projects/add_oem_camera.md).

## AsBuilt Configuration

The IPMB configuration listed here is derived from CyanLabs' notes, and not all of these settings appear to be functional on my vehicle. Some of them work and I've added notes for what I've observed.

| 07B1-01-01 | Nibble (hex) | Bit | Effect                            | Notes                          |
| ---------- | ------------ | --- | --------------------------------- | ------------------------------ |
|            | 0            | 0   | Drive side                        | 0 = Left, 1 = Right?           |
|            |              | 0   | Enable trailer backup assist      |                                |
|            |              | 0   | Enable front camera               |                                |
|            |              | 0   | Enable vehicle speed sensor sleep |                                |
|            | 0            | 0   | Rear camera type                  | 0 = VGA (C-Max), 1 = Megapixel |
|            |              | 0   | Front camera type                 | 0 = VGA (C-Max), 1 = Megapixel |
|            |              | 0   | Number of cameras                 | Note 2                         |
|            |              | 0   | Number of cameras                 |                                |
|            | 3            | 0   | Park assist type                  | Note 3                         |
|            |              | 0   | Park assist type                  |                                |
|            |              | 1   | Park assist type                  |                                |
|            |              | 1   | Park assist type                  |                                |
|            | 2            | 0   | Park assist display               | Note 3                         |
|            |              | 0   | Park assist display               |                                |
|            |              | 1   | Park assist display               |                                |
|            |              | 0   | Park assist display               |                                |
|            |              | -   |                                   |                                |
|            | 1            | 0   |                                   |                                |
|            |              | 0   |                                   |                                |
|            |              | 0   |                                   |                                |
|            |              | 1   | Vehicle park assist type          | Note 3                         |
|            | 3            | 0   | Slave exists FB                   |                                |
|            |              | 0   | Slave exists front view camera    |                                |
|            |              | 1   | Slave exists rear view camera     |                                |
|            |              | 1   |                                   |                                |
|            | 0            | 0   | LIN Select RVC                    | Note 4                         |
|            |              | 0   | LIN Select RVC                    |                                |
|            |              | 0   | LIN Select RVC                    |                                |
|            |              | 0   | LIN Select RVC                    |                                |
|            | 9            | 1   | LIN Select RVC                    |                                |
|            |              | 0   | LIN Select RVC                    |                                |
|            |              | 0   | LIN Select RVC                    |                                |
|            |              | 1   | LIN Select RVC                    |                                |
| CHECKSUM   | 08           |     | Autocalculated                    |                                |
| ---------- | ------------ | --- | ------------------------------ | --------------------------------------------------------- |
| 07B1-02-01 | Nibble (hex) | Bit | Effect                         | Notes                                                     |
|            | D            | 1   | Enable Sync APA Fix            | No effect, C-Max default 1                                |
|            |              | 1   | Enable door ajar indicator     | No effect, C-Max default 1                                |
|            |              | 0   | Rear visual park assist        | Note 5                                                    |
|            |              | 1   | Rear visual park assist        |                                                           |
|            | 5            | 0   | Main Image Content             | Note 5                                                    |
|            |              | 1   | Main Image Content             |                                                           |
|            |              | 0   | Zoom level                     | Note 5                                                    |
|            |              | 1   | Zoom level                     |                                                           |
|            | 0            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            | 2            | 0   | Enable Raptor Mode             | [SCREECHING](https://www.youtube.com/watch?v=IxQl9-On6oQ) |
|            |              | 0   | FB Close Behavior              | May not be accurate                                       |
|            |              | 1   | Enable front camera indicator  | May not be accurate, set to 1 on C-Max?                   |
|            |              | 0   | Enable Tailgate ajar indicator | May not be accurate                                       |
|            |              | -   |                                |                                                           |
|            | 0            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            | 1            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 1   |                                |                                                           |
|            | 0            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            | 3            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 1   |                                |                                                           |
|            |              | 1   |                                |                                                           |
|            |              | -   |                                |                                                           |
|            | 0            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            | 0            | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
|            |              | 0   |                                |                                                           |
| CHECKSUM   | 96           |     | Autocalculated                 |                                                           |
| ---------- | ------------ | --- | ----------------- | ------ |
| 07B1-02-02 | Nibble (hex) | Bit | Effect            | Notes  |
|            | 0            | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            | 0            | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            | 0            | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            | 0            | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
|            |              | 0   | Reserved          |        |
| CHECKSUM   | BC           |     | Autocalculated    |        |
| ---------- | ------------ | --- | ----------------- | ------ |
| 07B1-03-01 | Nibble (hex) | Bit | Effect            | Notes  |
|            | 5            | 0   | "DTC Suppression" | Note 1 |
|            |              | 1   |                   |        |
|            |              | 0   |                   |        |
|            |              | 1   |                   |        |
|            | 9            | 1   |                   |        |
|            |              | 0   |                   |        |
|            |              | 0   |                   |        |
|            |              | 1   |                   |        |
|            | C            | 1   |                   |        |
|            |              | 1   |                   |        |
|            |              | 0   |                   |        |
|            |              | 0   |                   |        |
|            | 8            | 1   |                   |        |
|            |              | 0   |                   |        |
|            |              | 0   |                   |        |
|            |              | 0   |                   |        |
| CHECKSUM   | DD           |     | Autocalculated    |        |

### Note 1: Block 03-01

I'm not convinced this is 'DTC Suppression' on a C-Max, I suspect it manages other things. Without more info on what it does I'm afraid to experiment.

### Note 2: Number of cameras

This is a lookup table using the two bits:

* 00 = 1 camera (C-Max default)
* 01 = [2 cameras](https://knowyourmeme.com/memes/gee-bill-how-come-your-mom-lets-you-eat-two-wieners)
* 10 = 4 cameras
* 11 = Reserved

### Note 3: Park assist type

The C-Max came with three options for park assist: none, backup only, and 12 channel. It's possible the last year with BLIS inlcudes 12 channel with flank but I've not found an AsBuilt configuration that includes that. I [don't plan on attempting to add BLIS](/projects/add_blis.md) so I don't know.

These values, thus, are dependent on what your vehicle has configured. They're also dependent on model year due to the camera communication change post-facelift.

#### Park assist type

This is a lookup table for the nibble value

* 0 = None (C-Max with no PDC sensors / no PAM)
* 2 = 4 channel
* 3 = 3 channel (C-max with only rear PDC sensors)
* 4 = 8 channel
* 6 = 10 channel
* 8 = 12 channel
* A = 12 channel with Flank

#### Park assist display

Not certain what this controls. This value is for the nibble.

* 0: Disabled
* 1: Rear Visual Park Assist
* 2: Full Visual Park Assist
* 3: Overhead Visual Park Assist
* Other values: Reserved

#### Vehicle parking assist type

This seems to control the communication channel to the camera.

* 0: Camera
* 1: IPMB (2013-2015 C-Max)

### Note 4: LIN Select RVC

This sets the LIN bus address for the RVC. Maybe. Possibly. It's entirely unclear.

These values are for the full byte.

* 09 - 2013-2015 C-Max default
* 33 - Different display mode?
* 61 - Different display mode?

Random spot checks for this value didn't seem to yield anything interesting. More research necessary.

Changing this value causes a temporary IPMB DC B115E:54-48 Missing Calibration

### Note 5: Memory settings

These settings appear to control the default state of features when the vehicle is turned on.

* Rear VPA: Overlay lines on the screen?
* Main Image Content: Maybe whether the screen displays at all?
* Zoom Level: Zoomed in or not.

The settings are for two bytes:

* 00: Off
* 01: On (C-max default for all three settings)
* 10: Last Known
* 11: Factory Off (Disabled?)
