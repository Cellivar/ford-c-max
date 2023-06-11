# Central Configuration

C1MCA vehicles make use of a Central Configuration (CC) block, a special config block usually in the [BdyCM](/systems/modules/BdyCM.md) that is distributed to other modules on the network. Those modules then react according to the CC settings. It's speculated this was driven by early cost-cutting measures on the C1-platform vehicles. If 5 modules can save on cost by not having non-volatile storage for AsBuilt configs then it's cheaper-per-car to have a CC instead.

Ford CGEA vehicles use distributed configuration blocks in all modules, that is, if a module needs to have a configuration value set then that module will have a [module-level config exposed as an AsBuilt flag on that module](./ford_module_config.md).

The C-Max, being in a weird transition period on top of being a weird vehicle, has _both_ a Central Configuration for many settings _and_ individual module configurations. Even better, sometimes Central Configuration values are _ignored_ in favor of module configurations that perform similar functions.

I'm sure there's a fascinating internal tech debt story at Ford about this period of time that nobody will ever re-tell.

## Central Config Storage and Programming

The primary CC is stored in the [BdyCM](/systems/modules/BdyCM.md) and a secondary backup is stored in the [IPC](/systems/modules/IPC.md). Supposedly if the main one is corrupt the BdyCM will download the backup copy from the IPC to restore it, or something. I have never witnessed this happen, the FORScan devs seem to think it doesn't happen after 2007-ish-era vehicles, and more modern vehicles don't have a backup at all.

This means the only one you ever really need to touch is the primary. Don't mess with the backup in the IPC.

WHEN PROGRAMMING THE CC YOUR CAR WILL FREAK OUT. The CC is a special programming block that needs to be done after putting the CANBus network in a special communication state. DO NOT attempt this while driving. MAKE SURE YOUR 12V BATTERY IS READY TO GO. DO NOT attempt this if you need to be somewhere in a hurry. You may generate DTCs during programming because of the mode, they can be cleared after programming. [See this FORScan thread for more](https://forscan.org/forum/viewtopic.php?t=1932).

## Relevant settings

The vast majority of the Ford CC settings should be set to a specific value for a C-Max and never changed, a lot of the settings have to do with PATS key programming, vehicle dynamics, and other things no individual would want to mess with.

To generate this list I started looking for used vehicles online that appeared to have the various features I wanted. Since the equipment groups 301, 302, and 303 shipped with multiple clear indicators I was able to find relevant vehicles, get their VIN, run it through Ford's AsBuilt tool, and dump the raw CC values into a spreadsheet for comparison. [This CSV file is the result of that.](/systems/modules/configs/cc.csv) Review the full list for what all of the settings mean.

FORScan won't show you the raw byte numbers, but if you set the Central Config viewer settings to "Engineering +2" menu it will show all of the values in order. You can also use search to find the values. Not all values noted here are allowed to be set by FORScan.

ALWAYS SAFE A BACKUP OF YOUR CONFIGURATION BEFORE YOU CHANGE SOMETHING. JUST IN CASE. IT IS ALWAYS WORTH IT.

### Interesting settings

These are settings you may want to change.

| Setting                          | Byte | Notes                                                                                 |
| -------------------------------- | ---- | ------------------------------------------------------------------------------------- |
| Headlights, type                 | 14   | 02 = Halogen 2013-2015, 18 = LED 2016+                                                |
| Daytime Running Lights           | 16   | Note 1                                                                                |
| Foglight function                | 18   | Note 2                                                                                |
| BLIS                             | 37   | 01 = No BLIS, 03 = With BLIS (2017)                                                   |
| Parking Assistance               | 59   | 02 = Rear only, 05 = [SAPP](/projects/add_parallel_park.md)                           |
| Roof type                        | 66   | 01 = Metal, 02 = Panoramic. IF YOU INSTALL THIS SHOW ME PICTURES.                     |
| Loudspeaker quantities           | 73   | 02 = Standard, 09 = Sony premium audio                                                |
| Park assist camera               | 99   | 01 = No camera, 02 = [With camera](/projects//add_oem_camera.md)                      |
| Roof hatch                       | 108  | 01 = With panoramic roof, 02 = No panoramic roof                                      |
| In car entertainment             | 112  | 17 = Standard, 18 = With Sony                                                         |
| Center speaker, dashboard        | 120  | 00 = 2016+?, 01 = Standard (disabled), 02 = Sony (enabled)                            |
| Self opening tailgate            | 177  | 01 = None, 03 = [With powered liftgate](/projects/add_power_liftgate.md)              |
| Door remote control channel type | 186  | 02 = Non-IAK/PEPS, 04 = With IAK/PEPS (5 button remote)                               |
| Wheel speed sensor type          | 203  | 01 = With autopark (bidirectional sensors), 02 = No autopark (unidirectional sensors) |

#### Note 1 - Daytime Running Lights

My 2013 model is a fleet vehicle and had DRLs enabled from the factory according to my Monroney sticker. You can pay Ford to change this setting for you, or you can change it in FORScan. There are 4 applicable settings for a C-Max:

* 02 = Always dipped lights (standard DRLs)
* 03 = Always dipped except in position P (this does not turn them off in park)
* 05 = Default for 2017
* 0A = Default for 2015

It's not clear what the differences are for 2015+ models, and I can't test them on my 2013 vehicle.

Some models of cars are able to configure the DRL setting via the IPC. This does not seem to work for 2013 vehicles.

The recommended workaround is to install a switch on the headlight fuse that can be used to toggle them off when you're, say, slowly driving through a drive-in movie theatre and don't want to annoy the crap out of others. Ask me how I know.

#### Note 2 - Foglight function

By default a C-Max does not allow high beams with fog lights. You can alter this setting to enable that:

* 01 - No fog lights
* 02 - Enabled with no restrictions ("bambi mode")
* 03 - Enabled, disabled with high beams (Default)

### Unclear settings

These settings are different with no obvious need to be. They are usually related to the 2016 facelift differences and likely relate to differences in the BdyCM firmware that are undocumented.

| Setting                             | Byte | Notes                                                                       |
| ----------------------------------- | ---- | --------------------------------------------------------------------------- |
| Battery                             | 210  | 09, 00, unclear effect                                                      |
| Integrated Control Panel            | 214  | 08 With Sony?, 09 = Less Sony?, unclear effect                              |
| Fuel Type                           | 6    | 03 = FHEV, 08 = PHEV (Energi)                                               |
| Fuel tank volume                    | 11   | 0B = FHEV? 0D = PHEV Energi?, not entirely certain, should be same?         |
| Wheel brakes type front             | 46   | 01 = 2013-2014, 0C 2015+, unclear differences/effect                        |
| Telephone                           | 50   | 01 = FHEV, 05 = PHEV, maybe TCU?                                            |
| Tire circumference                  | 51   | 04 = 2013, 05 = 2014+, should be 17" for all years??                        |
| Frequency - Remote controls         | 63   | Note 1, 01 = IAK?? 2013-2014, 24 = 2015 non-IAK???                          |
| Final drive ratio                   | 71   | 66 = 2013 (2.91), 0D = 2014+ (2.75, part of MPG changes??)                  |
| Suspension                          | 74   | 01 = 2013-2014, 19 = 2015+, shouldn't be different??                        |
| Integrated vehicle dynamics control | 75   | 09 = 2013-2015 (ESP wo/HLA), 06 = 2016+ (Enhanced ESP/IVD) ??               |
| Bluetooth handsfree                 | 157  | 08 = Less Nav/Sony, 09 = Withy Nav/Sony                                     |
| Door remote control channel type    | 186  | Note 1, 02 = Less IAK (3 button remote/key?), 04 = With IAK/PEPS (5 button) |
| Aesthetic Lighting                  | 216  | Note 2                                                                      |
| Remote Start                        | 242  | Note 1,01 = Less IAK (3 button remote/key?), 02 = With IAK/PEPS (5 button)  |

#### Note 1: Remote controls and Remote Start

From what I can tell there were 2 possible keys:

* Intelligent Access Key (IAK) 5-button remote with Passive Entry / Passive Start (PEPS), push-button start.
* 3-button key with standard ignition

The IAK was part of the SEL package and included a lot of other features, so sometimes it's hard to piece out the individual differences. Several settings directly related to IAK vs non-IAK. Theoretically one could upgrade a C-Max from the standard key to an IAK/PEPS system, but given the general pain-in-the-rear PATS key programming, several additional modules and antennas to add, and cost of everything associated it sounds fairly daunting.

#### Note 2: Aesthetic Lighting

The post-facelift 2016+ years changed how the ambient lighting communication happened. They moved the control of the lights off of a hardware system (with a button to change the color on the headliner console) to a CAN-connected controller. Sync 3 added a menu to be able to select one of several ambient lighting colors.

* 03 = 2013-2015 (Hardware Ambient)
* 01 = 2016+ None,
* 05 = 2016+ (CAN Ambient)

## Sources

* [FoCCCus central configuration decoder](http://ford.xtlt.ru/ab/)
* [FORScan thread on CC](https://forscan.org/forum/viewtopic.php?t=1932)
