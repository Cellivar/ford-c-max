# Ford C-Max Systems

The Ford C-Max is a bonkers mishmash of late-era C-Platform systems smashed together with cutting edge design with a lot of hopeful, excited Ford engineers building something cool. This documentation is for the systems that make up the car and quirks/details about those systems that are relevant.

## Primary Modules

These module names come from ForScan, which may or may not coincide with Ford documentation. If you have suggestions for names let me know!

| Code                          | Name                                   | Description                                                                                                                       |
| ----------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [SOBDMC](./modules/SOBDMC.md) | Secondary OBD Control Module C         | Hybrid/transmission control module                                                                                                |
| [BECM](./modules/BECM.md)     | Battery Energy Control Module          | High voltage, not the 12V                                                                                                         |
| [SOBDM](./modules/SOBDM.md)   | Secondary OBD Control Module A         | Onboard PHEV charger (Energi only)                                                                                                |
| [PCM](./modules/PCM.md)       | Powertrain Control Module              |                                                                                                                                   |
| [OBDII](./modules/OBDII.md)   | On Board Diagnostic II                 |                                                                                                                                   |
| [APIM](./modules/APIM.md)     | Accessory Protocol Interface Module    | The 'head unit' touchscreen/Sync module                                                                                           |
| [ACCM](./modules/ACCM.md)     | Air Conditioning Control Module        |                                                                                                                                   |
| [GFM](./modules/GFM.md)       | Generic Function Module                | Charge port light ring (Energi only)                                                                                              |
| [SASM](./modules/SASM.md)     | Steering Angle Sensor Module           |                                                                                                                                   |
| [OCS](./modules/OCS.md)       | Occupant Classification System Module  |                                                                                                                                   |
| [ABS](./modules/ABS.md)       | Antilock braking system                |                                                                                                                                   |
| [DCDC](./modules/DCDC.md)     | DC to DC Converter Control Module      | Mimics/replaces a traditional alternator, converts power from<br />the traction battery down to the 12-14V for accessory systems. |
| [RCM](./modules/RCM.md)       | Restraint Control Module               |                                                                                                                                   |
| [PAM](./modules/PAM.md)       | Parking Aid Module                     | If equipped with parking distance sensors                                                                                         |
| [PSCM](./modules/PSCM.md)     | Power Steering Control Module          |                                                                                                                                   |
| [BdyCM](./modules/BdyCM.md)   | Body Control Module                    | Brainbox, many subsystems                                                                                                         |
| [GWM](./modules/GWM.md)       | Gateway Module A                       | A router of sorts                                                                                                                 |
| [DACMC](./modules/DACMC.md)   | Digital Audio Control Module C         | Audio amplifier/Active noise cancellation system                                                                                  |
| [IPMB](./modules/IPMB.md)     | Image Processing Module B              | Backup camera, if equipped                                                                                                        |
| [FCIM](./modules/FCIM.md)     | Front Controls Interface Module        | Physical radio controls (8-inch touch screen equipped vehicles)                                                                   |
| [FCDIM](./modules/FCDIM.md)   | Front Control/Display Interface Module | 4-inch non-touch screen/controls on lower trim vehicles                                                                           |
| [TCU](./modules/TCU.md)       | Telematic Control Unit Module          | Cellular modem, either 2g, 3g, 4g (Energi only)                                                                                   |
| [PDM](./modules/PDM.md)       | Passengers Door Control Unit           |                                                                                                                                   |
| [DDM](./modules/DDM.md)       | Drivers Door Module                    |                                                                                                                                   |
| [HVAC](./modules/HVAC.md)     | Heating Ventilation Air Conditioning   |                                                                                                                                   |
| [RFA](./modules/RFA.md)       | Remote Function Actuator               |                                                                                                                                   |
| [ACM](./modules/ACM.md)       | Audio Control Module                   | AM/FM/CD/Sirius tuner/audio routing module                                                                                        |
| [IPC](./modules/IPC.md)       | Instrument Panel Control Module        |                                                                                                                                   |
| [GPSM](./modules/GPSM.md)     | Global Positioning System Module       |                                                                                                                                   |
| [RGTM](./modules/RGTM.md)     | Rear Gate Trunk Module                 | Powered liftgate controller, if equipped                                                                                          |

## System Information

* [Vehicle specs](./specs.md)

### Electrical

* [12V Battery](./electrical/low_voltage_battery.md)

## General Information

* [Ford electrical platform overview](./ford_platform_overview.md)
* [Ford parts numbers overview](./ford_vin.md)
