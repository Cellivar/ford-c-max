# Instrument Panel Cluster

Original (that came with my car)

| Module Property     | Value                | Notes |
| ------------------- | -------------------- | ----- |
| AsBuilt Module Code | 720                  |       |
| Part number         | DM5T-10849-EL        |       |
| Calibration         | DM5T-14C088-CJ       |       |
| Strategy            | DM5T-14C026-CJ       |       |
| Calibration Level   | DM5T-10849-EL        |       |
| Location            | Above steering wheel |       |
| Bus                 | MS-CAN, I-CAN        |       |

New retrofit

| Module Property     | Value                | Notes |
| ------------------- | -------------------- | ----- |
| AsBuilt Module Code | 720                  |       |
| Part number         | HM5T-10849-AC        |       |
| Calibration         |                      |       |
| Strategy            |                      |       |
| Calibration Level   |                      |       |
| Location            | Above steering wheel |       |
| Bus                 | MS-CAN, I-CAN        |       |

⚠️⚠️⚠️ DO NOT ATTEMPT TO UPDATE FIRMWARE WHILE INSTALLED IN THE VEHICLE ⚠️⚠️⚠️

For reasons that are not well understood [FORScan cannot reliably update the firmware of C-Max IPCs](https://forscan.org/forum/viewtopic.php?p=70432&sid=8a79e46f2dace6f8e82e992572df1b67#p70432) while installed in the vehicle.

If you wish to update the firmware of a C-Max IPC you must remove it from the vehicle and flash it there.

1. First use FORScan to create a vehicle profile for your vehicle while the IPC is installed. Save the profile.
2. Remove the IPC.
3. Wire the IPC up on a bench using the note below.
4. Connect FORScan to the module using the saved profile, it should be able to communicate to the IPC.
5. Proceed with the firmware update.

Pins 12 and 13 should be 120 ohms in this configuration.

The IPC pins can be connected:

* Pin 21 - 12V
* Pin 5 - Ground
* Pin 12 - MS-CAN+ (pin 3 of the OBDII connector)
* Pin 13 - MS-CAN- (Pin 11 of the OBDII connector)

This issue is confirmed present on D-series and F-series parts. I'm not willing to test on my H-series unit.

## Engineering Test Mode

Engineering Test Mode can be used to quickly check the IPC for issues and for part numbers.

1. Start with the engine off and the screen off.
2. Press and hold the OK button on the left D-Pad on the steering wheel.
3. Start the car.
4. Continue holding the button until you see a yellow "ET" appear in the top left of the left screen. This will show even if there are other popups present.
5. Release as soon as you see the "ET" appear.

You can scroll through the screens with the left D-Pad. Press and hold OK to exit ET mode.

<img src="https://github.com/Cellivar/ford-c-max/assets/1441553/b1907ec2-4d11-401f-a74b-1973bfc582d3" width="200px"/>

<img src="https://github.com/Cellivar/ford-c-max/assets/1441553/e2b6c48b-7116-4c4b-820c-525bd8e3a105" width="200px"/>


## Part Number Notes

The IPC is a sandwich of 3 different parts:

* CV6Z-10890-B - The bezel with chrome trim, for all years and the Focus BEV.
* CV6Z-10890-A - The plastic lens/dust cover, for all years and the Focus BEV.
* The cluster display board, with the speedo and screens, the prefix ends in a Z.

These three parts _together_ make up the _assembly_ part number that ends in a T. For example a DM5T-10849-EL is the _assembly_ part number for the complete 3-piece sandwich assembly, including a DM5Z-10849-EL cluster display board. Same deal with an HM5Z-10849-AC board and HM5T-10849-AC assembly.

Why does this matter? _Most part websites don't have the assembly, they only have the individual parts._ A google search for `DM5T-10849-EL` will [show stuff from used resellers, usually](https://www.google.com/search?q=DM5T-10849-EL). A search for `DM5Z-10849-EL` instead [shows where you can buy them new](https://www.google.com/search?q=DM5Z-10849-EL). Removing the last two letters also improves hit counts. Be aware of this difference (and lack of information) when researching or looking for part numbers.

### Part number differences

There are several C-Max model number prefixes that were used for assemblies and boards. It's not clear what Ford used the different model numbers for, or precisely what years they all apply to. The parts websites are all over the place on what submodules exist, what they're available for, etc.

* D-series, like `DM5T-10849-EL`
* F-series, like `FM5T-10849-CE`
* G-series, like `GM5T-10849-AC`
* H-series, like `HM5T-10849-AC`

This is a table of part numbers and what years they were encountered on. It [seems to line up with the Ford Part Number Format](/tools/ford_part_numbers.md).

| Part Numbers  | Known Years              |
| ------------- | ------------------------ |
| DM5T-10849-EL | 2013                     |
| HM5T-10849-AC | 2017                     |
| GM5T-10849-AC | 2016                     |
| GM5T-10849-DA | 2016-2018 Focus Electric |
| FM5T-10849-CE | 2015                     |

The model series seems to generally determine what the software behavior is like. Here's a table of screenshots for different versions.

<details>
<summary>Visual comparison of screenshots between versions</summary>

| Screen Name | DM5T | FM5T | GM5T | HM5T |
| ----------- | ---- | ---- | ---- | ---- |
|             |      |      |      |      |

</details>

### D-series

* 2013 design year

The DM5T doesn't have a second 720-02 AsBuilt block.

The DM5T has MPGe support, that is, the software allows configuring the mileage calculation to either _exclude_ all electric driving from the MPG displays, or _including_ your EV driving efficiency as part of MPGe calculation.

Without MPGe calculation support your MPG will be "999" at the end of an all-electric drive. Later models of IPC did away with this feature. The speculated reason is to help bump up the perceived MPG efficiency of the vehicle after the EPA MPG fiasco.

Original AsBuilt for my car:

```
720-01-01 2120 6047 394A
720-01-02 CCDC 7860 3BE5
720-01-03 9001 06C8 29B3
720-01-04 ADD9
```

### F-series

* 2015 design year

Unknown!

### G-series

* 2016 design year

Unknown!

### H-series

* 2017 design year

* 2017-2018

The HM5T includes the second 720-02 block of AsBuilt config.

The HM5T does not calculate MPGe, all displayed MPG values exclude EV driving efficiency entirely, treating EV distance as "completely free".

The green and yellow colors of the HM5T are much more saturated than the DM5T, making them easier to read.

An AsBuilt for a 2017 Energi Titanium w/autopark sensors, Nav, Sony Audio:

```
720-01-01 	2120 	6447 	394E
720-01-02 	CCDC 	3860 	3BA5
720-01-03 	9801 	06F8 	29EB
720-01-04 	AFDB
720-02-01 	5553 	8270 	00C4
720-02-02 	0000 	002B
```

## AsBuilt Configuration

| 0720-01-01 | Nibble (hex) | Bit | Effect                                        | Notes                                   | FORScan name                |
| ---------- | ------------ | --- | --------------------------------------------- | --------------------------------------- | --------------------------- |
|            | 2            | 0   | Fuel tank capacity                            | Note 1                                  |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 1   | Fuel tank capacity                            |                                         |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            | 1            | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 1   | Fuel tank capacity                            |                                         |                             |
|            | 2            | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            |              | 1   | Fuel tank capacity                            |                                         |                             |
|            |              | 0   | Fuel tank capacity                            |                                         |                             |
|            | 0            | 0   | Enable second fuel sender                     | 0 = 1, 1 = 2                            |                             |
|            |              | 0   | Enable second fuel tank                       | 0 = 1, 1 = 2                            |                             |
|            |              | 0   | Enable Flex Fuel                              | No effect?                              | Flex Fuel                   |
|            |              | 0   | Enable manual transmission type               | 0 = Auto, 1 = Man                       | Transmission Type           |
|            | 6            | 0   | Enable adjustable speed limiter device        | ???                                     |                             |
|            |              | 1   | Enable Eco Cruise setting                     | Note 2                                  | Eco Speed                   |
|            |              | 1   | IPC clock display enable                      | Note 3                                  | Global Clock                |
|            |              | 0   | Hill Start Assist                             | Note 4                                  |                             |
|            | 4            | 0   | Enable auto engine idle shutdown w/o override |                                         |                             |
|            |              | 1   | Enable auto engine idle shutdown w/ override  |                                         |                             |
|            |              | 0   | Hybrid Mode                                   | 0 = PHEV, 1 = FHEV                      |                             |
|            |              | 0   | Enable Perimeter Alarm Reduced Guard          |                                         |                             |
|            | 4            | 0   | Display 24 hour time instead of 12            | Note 3                                  | Global clock display format |
|            |              | 1   | EV Enhanced GPS                               |                                         | EV Enhanced GPS             |
|            |              | 0   | Low washer fluid warning                      | No sensor on C-Max                      |                             |
|            |              | 0   | Enable Deflation Detection System             | C-Max uses TPMS instead                 |                             |
|            | 7            | 0   | Enable rear fog light indicator               | Not on North America C-Maxes            | Rear fog                    |
|            |              | 1   | Enable front fog indicator                    | Enables indicator                       | Front fog                   |
|            |              | 1   | Enable TPMS                                   | Low pressure warning, no PSI readout    |                             |
|            |              | 1   | Enable ABS                                    |                                         |                             |
|            | 3            | 0   | Enable DSP                                    | Not Sony DSP?                           |                             |
|            |              | 0   | Chime Generator Source                        | Note 5                                  |                             |
|            |              | 1   | Chime Generator Source                        |                                         |                             |
|            |              | 1   | EE Format Menu                                | ????                                    |                             |
|            | 9            | 1   | Key-in-ignition chime                         | No effect on keyless C-Maxes?           |                             |
|            |              | 0   | Enable overspeed chime                        |                                         |                             |
|            |              | 0   | Backup (Japan Only)                           | ???                                     |                             |
|            |              | 1   | Enable roll-stability chimes                  | Beeps when you're about to flip the car |                             |
| CHECKSUM   | 4E           |     | Autocalculated                                |                                         |                             |

| 0720-01-02 | Nibble (hex) | Bit | Effect                             | Notes                              | FORScan name                   |
| ---------- | ------------ | --- | ---------------------------------- | ---------------------------------- | ------------------------------ |
|            | C            | 1   | Driver beltminder                  |                                    |                                |
|            |              | 1   | Passenger beltminder               |                                    |                                |
|            |              | 0   | Mid-passenger beltminder           |                                    |                                |
|            |              | 0   | Speedo Calibration                 | 0 = NA, 1 = EU                     |                                |
|            | C            | 1   | Vehicle Control System             | Note 6                             |                                |
|            |              | 1   | Vehicle Control System             |                                    |                                |
|            |              | 0   | Vehicle Drivetrain                 | Note 6                             |                                |
|            |              | 0   | Vehicle Drivetrain                 |                                    |                                |
|            | D            | 1   | Enable MyKey menu                  |                                    |                                |
|            |              | 1   | Enable MyKey volume limit          |                                    |                                |
|            |              | 0   | Shutdown charge menu display       | Note 7                             | Show next charge               |
|            |              | 1   | Oil pressure switch                | 0 = HW, 1 = CAN                    |                                |
|            | C            | 1   | PEPS (Keyless)                     |                                    | Passive entry passive start    |
|            |              | 1   | Turn by turn navigation            | Enables compass and nav            | Turn by turn navigation        |
|            |              | 0   | Digital radio program type         | 0 = US, 1 = RDS                    |                                |
|            |              | 0   | TCM Present                        | Not for C-Maxes                    |                                |
|            | 3            | 0   | PDC popup menu - front             | No actual effect                   | Park Aid Menu - Front          |
|            |              | 0   | PDC popup menu - rear              | Show/hide rear sensor setting page | Park Aid Menu - Rear           |
|            |              | 1   | PT Hybrid Type                     | Note 8                             |                                |
|            |              | 1   | PT Hybrid Type                     |                                    |                                |
|            | 8            | 1   | Fuel consumed per hour display     | No effect                          |                                |
|            |              | 0   | Display cruise set speed           | Note 9 - worth enabling!           | Cruise Control Set Speed       |
|            |              | 0   | Enable cruise control menu         | No effect                          | Cruise control menu            |
|            |              | 0   | Display Units                      | 0 = SAE, 1 = Metric                |                                |
|            | 6            | 0   | CCC Parameter 93 Language          | 0 = English, 1 = Something else    |                                |
|            |              | 1   | Enable compass display             | Note 10                            | Compass                        |
|            |              | 1   | Enable welcome and goodbye screens | Note 11                            | Welcome and Farewell Screens   |
|            |              | 0   | Welcome on during crank            | Note 11                            | Welcome screen ON during crank |
|            | 0            | 0   | IPC Language Selection             | Note 12                            |                                |
|            |              | 0   | IPC Language Selection             |                                    |                                |
|            |              | 0   | Enable low battery warning         | No effect                          |                                |
|            |              | 0   | Enable frost telltale              | Can't test, California lol         |                                |
|            | 3            | 0   | Enable UK Gallons                  | UK gallons as display unit         |                                |
|            |              | 0   | Metric fuel display type           | 0 = L/100km, 1 = km/L              |                                |
|            |              | 1   | Enable outside air temp display    | Note 13                            | Outside air temperature        |
|            |              | 1   | Enable IOLM                        |                                    | Oilminder                      |
|            | B            | 1   | Rear door configuration            | Note 14                            |                                |
|            |              | 0   | Rear door configuration            |                                    |                                |
|            |              | 1   | Enable tire kit minder             |                                    |                                |
|            |              | 1   | Enable EPAS power steering         | All C-Maxes have EPAS              |                                |
| CHECKSUM   | A5           |     | Autocalculated                     |                                    |                                |

| 0720-01-03 | Nibble (hex) | Bit | Effect                               | Notes                        | FORScan name          |
| ---------- | ------------ | --- | ------------------------------------ | ---------------------------- | --------------------- |
|            | 9            | 1   | Enable AdvanceTrack                  |                              |                       |
|            |              | 0   | Enable Adaptive Headlamps            | Not on NA C-Maxes            |                       |
|            |              | 0   | Enable Auto Highbeam                 | Not on NA C-Maxes            |                       |
|            |              | 1   | Enable auto home light menu          | Show/hide settings page      | Autolamp Delay        |
|            | 8            | 1   | Enable autopark                      |                              | AutoPark              |
|            |              | 0   | Easy Entry                           | Not on NA C-Maxes            |                       |
|            |              | 0   | Enable Global Open                   | No effect, controlled by CCC |                       |
|            |              | 0   | Enable Global Close                  | No effect, controlled by CCC |                       |
|            | 0            | 0   | Enable two-stage unlock              | No effect, controlled by CCC |                       |
|            |              | 0   | Enable autolock                      | No effect, controlled by CCC |                       |
|            |              | 0   | Enable auto-unlock                   | No effect, controlled by CCC |                       |
|            |              | 0   | CCC Parameter 62                     | 0 = Ford NA, 1 = Non-FNA     |                       |
|            | 1            | 0   | Enable courtesy wipers               | No effect, controlled by CCC |                       |
|            |              | 0   | Enable rain-sensing wipers           | No effect, controlled by CCC |                       |
|            |              | 0   | Enable reverse-gear wiper            | No effect, controlled by CCC |                       |
|            |              | 1   | Enable perimeter alarm               | Always set to 1?             |                       |
|            | 0            | 0   | Enable rear vehicle camera (RVC)     | No effect, controlled by CCC | Rear vehicle camera   |
|            |              | 0   | Enable camera delay                  | No effect, controlled by CCC | Camera - Delay        |
|            |              | 0   | Enable camera park aid               | No effect, controlled by CCC | Camera - Park Aid     |
|            |              | 0   | Enable camera zoom                   | No effect, controlled by CCC | Camera - Zoom         |
|            | 6            | 0   | Enable camera active guide           | No effect, controlled by CCC | Camera - Active Guide |
|            |              | 1   | Neutral Tow                          | Unclear effect?              |                       |
|            |              | 1   | Enable position side marker          | ????                         |                       |
|            |              | 0   | Enable RBM FoE Strategy              | ????                         |                       |
|            | F            | 1   | Enable Remote Start                  | Show/hide remote start menu  |                       |
|            |              | 1   | Enable remote start climate settings |                              |                       |
|            |              | 1   | Enable remote start driver seat      |                              |                       |
|            |              | 1   | Enable remote start passenger seat   |                              |                       |
|            | 8            | 1   | Enable remote start rear defrost     |                              |                       |
|            |              | 0   | Enable remote start steering wheel   | No heated steering wheel     |                       |
|            |              | 0   | Enable Distance-to-empty ascending   | Unclear effect??             |                       |
|            |              | 0   | Enable fuel operated heater          | N/A to C-Max                 |                       |
|            | 2            | 0   | MyView timeout seconds               | Note 15                      |                       |
|            |              | 0   | MyView timeout seconds               |                              |                       |
|            |              | 1   | MyView timeout seconds               |                              |                       |
|            |              | 0   | MyView timeout seconds               |                              |                       |
|            | 9            | 1   | MyView timeout seconds               |                              |                       |
|            |              | 0   | MyView timeout seconds               |                              |                       |
|            |              | 0   | MyView timeout seconds               |                              |                       |
|            |              | 1   | Enable AM/FM Menu                    | Note 16                      |                       |
| CHECKSUM   | EB           |     | Autocalculated                       |                              |                       |

| 0720-01-04 | Nibble (hex) | Bit | Effect                    | Notes   | FORScan name |
| ---------- | ------------ | --- | ------------------------- | ------- | ------------ |
|            | A            | 1   | Enable CD Menu            | Note 16 |              |
|            |              | 0   | Enable DAB Menu           | Note 16 |              |
|            |              | 1   | Enable SirisXM Menu       | Note 16 |              |
|            |              | 0   | Enable Climate menu       | Note 17 |              |
|            | F            | 1   | Enable Emotive Menu       | Note 18 |              |
|            |              | 1   | Enable Entertainment Menu | Note 16 |              |
|            |              | 1   | Enable Navigation Menu    | Note 19 |              |
|            |              | 1   | Enable Phone Menu         | Note 20 |              |
| CHECKSUM   | DB           |     | Autocalculated            |         |              |

| 0720-02-02 | Nibble (hex) | Bit | Effect                       | Notes                                                 | FORScan name |
| ---------- | ------------ | --- | ---------------------------- | ----------------------------------------------------- | ------------ |
|            | 5            | 0   | Language Code                | Note 21                                               |              |
|            |              | 1   | Language Code                | [Country Code](/systems/modules/ford_country_code.md) |              |
|            |              | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            | 5            | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            |              | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            | 5            | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            |              | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            | 3            | 0   | Language Code                |                                                       |              |
|            |              | 0   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            |              | 1   | Language Code                |                                                       |              |
|            | 8            | 1   | Enable HD Radio              |                                                       |              |
|            |              | 0   | Europe/Non-Europe            | 0 = Non-EU, 1 = EU                                    |              |
|            |              | 0   | Hourly fuel display          | 0 = Graph, 1 = Numeric, no effect                     |              |
|            |              | 0   | TPMS FedReg Config           | 0 = FMVSS138, 1 = ECE64 (EU)                          |              |
|            | 2            | 0   | Enable DRL Menu              | Note 22                                               |              |
|            |              | 0   | Enable Home Range Warning    | ???                                                   |              |
|            |              | 1   | Enable Fuel History Display  |                                                       |              |
|            |              | 0   | Enable Eco Mode RTT          |                                                       |              |
|            | 7            | 0   | Enable Grade Assist Menu     | Note 23                                               |              |
|            |              | 1   | Enable Next Full Charge      | Note 7                                                |              |
|            |              | 1   | Enable Cross-Traffic Alert   | Note 24                                               |              |
|            |              | 1   | Enable Side Detect           | Note 24                                               |              |
|            | 0            | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   | Enable Compass Sync 3 Source | Note 25                                               |              |
|            | 0            | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            | 0            | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   |                              |                                                       |              |
|            |              | 0   | Enable Approach Detection    | Note 26                                               |              |
| CHECKSUM   | C4           |     | Autocalculated               |                                                       |              |

| 0720-02-02 | Nibble (hex) | Bit | Effect         | Notes   | FORScan name |
| ---------- | ------------ | --- | -------------- | ------- | ------------ |
|            | 0            | 0   |                | Note 27 |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            | 0            | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            | 0            | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            | 0            | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            | 0            | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            | 0            | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
|            |              | 0   |                |         |              |
| CHECKSUM   | 2B           |     | Autocalculated |         |              |

### Note 1: Fuel tank capacity

The fuel tank capacity, in liters, multiplied by 10.

For example, the value 0x212 is 530 in decimal. Divide that by 10 to get 53, then divide by 3.785 to get 14 gallons, the capacity of the C-Max fuel tank.

All C-Maxes use the same 53 liter / 14 US gallon fuel tank.

This is used for range estimation calculations and possibly other things. Unclear why you'd want to change it.

### Note 2: Eco Cruise

One of the selling points of the C-Max is 'Eco Cruise', a setting whereby the vehicle will gracefully throttle back up to the cruise control set point.

For example, let's say cruise is set to 45 and you're accelerating from a red light

1. You start accelerating.
2. As soon as you hit 20 MPH (the cruise cutoff limit) you pull the cruise resume paddle.
3. The vehicle will throttle up to the second bar on the power meter and not exceed this much to approach 45 MPH.

The vehicle will dynamically adjust power input based on determined acceleration. If you're going up a hill at speed the vehicle will pour on more power, smoothly, to try and maintain your speed.

This setting enables a menu to enable or disable this feature. I strongly recommend leaving it on.

### Note 3: IPC Clock

On DM5T units the right screen has space for a clock on the bottom bar. This setting controls whether this clock is displayed.

The 'Display Format' lets you control whether this is a 12-hour clock or 24-hour clock.

On HM5T units the clock is replaced by a DTE estimate for fuel and electrons, so these two settings don't affect the display.

### Note 4: Hill Start Assist

On DM5T units this doesn't appear to do anything for the IPC.

On HM5T units a popup will display when hill-hold is active.

Hill-hold is when you come to a dead stop on an incline. The vehicle will automatically hold the brakes for you for a few moments while your foot moves off of the brakes and onto the accelerator. It will continue to apply the brakes until you depress the accelerator pedal until the vehicle can begin moving forward.

Having driven around San Francisco and Seattle with my C-Max I found this feature to be very helpful!

### Note 5: Chime Generator Source

These two bits configures where the vehicle is supposed to route audio for chimes.

* 00: IPC Speaker Only
* 01: IPC and Stereo (C-Max Default)
* 10: Stereo only
* 11: Not used

### Note 6: Vehicle Control System and Drivetrain

Vehicle Control System determines the type of signals the IPC should expect to need to display.

* 00: Disabled
* 01: Traction Control
* 10: Interactive Vehicle Dynamics
* 11: Roll Stability Control (C-Max Default)

The Drivetrain setting controls something about how the vehicle drives or something, dunno.

* 00: 2WD (C-Max default)
* 01: 4x4
* 10: AWD
* 11: Not used

### Note 7: Shutdown charge menu display

The 'Show Next Charge' screen shows on the right panel and displays when the vehicle will begin charging when you plug it in. You also get a menu to choose 'Value Charge' or 'Charge Now' to control this. This feature works as expected.

For some reason Ford decided to leave it disabled. It's confirmed working on DM5T and HM5T on my 2013 Energi.

Note that this replaces any other farewell screens on the right side. On the DM5T the default farewell screen is an animation of blowing leafs and a message saying "Thank you for driving a hybrid", which, like, _awww_.

On the HM5T the default farewell screen is the 'Next Full Charge' screen instead. It displays how your driving session went and what impacted your energy use on the trip. **On my 2013 Energi this doesn't work**, the graph is always empty. It appears to depend on information from a different module. The theory at time of writing (2023-06-04) is the Gateway Module is not sending data in the right format.

### Note 8: PT Hybrid Type

It's not clear what all this controls, but it seems to affect multiple screen elements such as the battery display.

* 00: Non-hybrid
* 01: BEV (Focus Electric)
* 10: FHEV
* 11: PHEV (Energi)

### Note 9: Display cruise set speed

I have absolutely no idea why Ford leaves this disabled, it works great and is nice to see. If you modify nothing else about your car _turn this on_.

### Note 10: Enable compass display

There are two things this controls. In the Navigation menu there is a compass display which shows a large compass.

There is a second compass direction indicator on the bar that this also enables or disables.

On DM5T modules the source for the compass is the GPSM. If you [retrofit a Sync 3 APIM](/projects/mod_sync_3.md) you must retain the GPSM to keep the compass working.

On HM5T modules the Sync 3 GPS is supposed to be the source, however I have doubts on whether this works properly on my 2013 Energy. See Note 25 for more details.

### Note 11: Enable welcome and farewell screens

The IPC screens are on both before and after the vehicle is running in either ACC or RUN modes. The contents displayed are referred to as 'welcome' and 'farewell' screens, and this setting enables or disables them.

When disabled this interferes with the other farewell screens, like the Next Charge and Next Full Charge screens from Note 7.

The related 'Welcome screen on during crank' setting would, in theory, also control how the screen is displayed. The problem is C-Maxes don't crank, they just turn on. If there is a 'crank' operation within that timespan I don't know and this setting doesn't appear to do anything.

### Note 12: IPC Language Setting

It's not clear how this setting relates to the Language Code setting in Note 21.

DM5T units do not have a Language Code, they only have the IPC Language Setting. Thus, this is the setting that controls the IPC language on DM5T units.

* 00: English
* 01: Spanish
* 10: French
* 11: [English](https://engrish.com/)?

### Note 13: Enable outside air temp display

There is an outside air temperature display on the status bar, this controls whether that shows up.

### Note 14: Rear door configuration

This probably controls what the IPC displays as an icon for the 'Liftgate Is Ajar' screen.

* 00: Door(s)
* 01: Liftgate / Liftglass
* 10: Liftgate (C-Max Default)
* 11: Trunk

### Note 15: MyView Timeout

It's not entirely clear what this controls based on the name this is how long the MyView screen will sit waiting for input.

Note that only 7 bits are used, the last bit is used for Note 16.

The default value of 0x0010100 is 14 hex, 20 decimal, and a 20 second timeout _sounds_ like it's correct.

### Note 16: Entertainment Menu

The Entertainment menu is the 'red' menu on the right screen. Disabling the menu hides the entire setting.

The AM/FM, CD, DAB, and SirisXM menu settings will add or remove entries from the sub-menus within the Entertainment screen. I use this to disable inputs (like SirisXM) that I don't use.

### Note 17: Climate Menu

This appears to be an abandoned feature. On both DM5T and HM5T units the screen doesn't work. Leave disabled.

### Note 18: Emotive / Fuel Efficiency Menu

On DM5T displays this menu is called 'Emotive', and the only thing it shows is the Efficiency Leaves.

On HM5T units this is the Fuel Efficiency menu. This also displays a Coach screen and a slightly different Fuel History screen.

Disabling this removes the menu entry entirely.

### Note 19: Navigation Menu

This controls the entire Navigation menu, including the compass display. For non-Nav Sync units that have a GPSM you can still enable this and get the compass display.

This sub-menu becomes useless when Android Auto or CarPlay is connected. When they are not connected the Navigation sub-menus allow setting destinations using the steering wheel D-Pad instead of the Sync touchscreen. This works for both Sync 2 and Sync 3.

When Sync is driving the navigation the Compass screen will switch to an active navigation display. This shows the next manoeuver, distance to destination, time to destination, and the speed limit (if in the map data).

When Android Auto is driving navigation it will only display the next manoeuver, the distance to destination and time to destination both show as 0.

Car Play is not capable of driving the IPC Navigation display.

### Note 20: Phone Menu

This controls display of the Phone menu. When the Sync unit is connected to a Bluetooth phone this has several sub-menus that can control the phone.

I don't.. ever use this. So I turned it off so it's not in the way.

### Note 21: Language Code

As part of the CGEA transition Ford started normalizing some of its global configuration into the IPC. This included the common country code system. [See the full table here](/systems/modules/ford_country_code.md).

The common codes for C-Maxes:

* 5553 - UNITED STATES OF AMERICA (US)
* 4341 - CANADA (CA)
* 4D58 - MEXICO (MK)

### Note 22: DRL Menu

On a C-Max the DRLs are managed by the [BdyCM](./BdyCM.md) in the Central Config. CGEA vehicles, lacking a Central Config, may support controlling the DRLs via this menu.

Unfortunately for us enabling this setting provides a greyed-out DRL menu entry on an HM5T. A DM5T doesn't do anything differently.

If you want to have toggle-able DRLs on a C-Max you probably have to wire a switch to a relay.

### Note 23: Grade Assist Menu

Enabling this setting adds a greyed-out menu for Grade Assist. It's not clear what this would control.

All C-Maxes have a hill descent control button on the side of the shift knob. When engaged the C-Max will more actively control the speed of the vehicle when descending a steep incline. When you have cruise control set it will try to match the speed, using aggressive regen when there's battery capacity to charge and even using engine braking when the battery is full. If you do not have cruise set it will use max regen to try and target around 20-25 MPH.

### Note 24: Cross-Traffic and Side Detect

The 2017 model year introduced BLIS (Blind Spot Information System) support for C-Maxes. This adds two radar units in the rear bumper that detect vehicles coming by (cross-traffic) when backing up and at your side (Side Detect) when changing lanes. The IPC will show a warning, sound an alert, and the Sync 3 unit will show a warning as well.

Enabling this feature when you do not have BLIS installed will generate a DTC and display a warning on the IPC at every startup.

BLIS requires support in the [BdyCM](./BdyCM.md) module and additional wires run from the rear bumper, so it's fairly difficult to retrofit on a non-2017 C-Max.

### Note 25: Compass Sync 3 Source

On DM5T modules the source for the compass is the GPSM. If you [retrofit a Sync 3 APIM](/projects/mod_sync_3.md) you must retain the GPSM to keep the compass working.

On HM5T modules the Sync 3 GPS is supposed to be the source, however I have doubts on whether this works properly on my 2013 Energy. When I attempt to set this bit to 1 FORScan returns an error about an invalid module configuration. This setting may not be correct or it may detect the GPSM in my vehicle and be sad about it.

Either way, I can't test this setting and I'm leaving it disabled and the GPSM in my vehicle.

### Note 26: Approach Detection

Lincoln vehicles first came out with this feature and then Ford vehicles got it. The vehicle will detect when your fob comes near the vehicle and automatically light up the lights.

When I attempt to set this setting FORScan returns an error about an invalid module configuration. I can't test this setting.

There is a related setting in the [Body Control Module](BdyCM.md) that may be related, and this may be a CGEA-only setting.

### Note 27: 720-02-02 Block

I can find no details on what this controls. All of the C-Maxes I've found have this set to all zeros for their config. I have't dug deeper into other models like the Fusion and Focus that may have values here. the CyanLabs database doesn't have this block.

## Sources

* [CyanLabs Database](https://cyanlabs.net/asbuilt-db/ipc-c-max-2012-2019-database/)
