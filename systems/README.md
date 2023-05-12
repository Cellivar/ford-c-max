# Ford C-Max Systems

The Ford C-Max is a bonkers mishmash of late-era C-Platform systems smashed together with cutting edge design with a lot of hopeful, excited Ford engineers building something cool. This documentation is for the systems that make up the car and quirks/details about those systems that are relevant.

## Primary Modules

These module names come from ForScan, which may or may not coincide with Ford documentation. If you have suggestions for names let me know!

| Code   | Name                                   | Description                                                                                                                       |
| ------ | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| SOBDMC | Secondary OBD Control Module C         | Hybrid/transmission control module                                                                                                |
| BECM   | Battery Energy Control Module          | High voltage, not the 12V                                                                                                         |
| SOBDM  | Secondary OBD Control Module A         | Onboard PHEV charger (Energi only)                                                                                                |
| PCM    | Powertrain Control Module              |                                                                                                                                   |
| OBDII  | On Board Diagnostic II                 |                                                                                                                                   |
| APIM   | Accessory Protocol Interface Module    | The 'head unit' touchscreen/Sync module                                                                                           |
| ACCM   | Air Conditioning Control Module        |                                                                                                                                   |
| GFM    | Generic Function Module                | Charge port light ring (Energi only)                                                                                              |
| SASM   | Steering Angle Sensor Module           |                                                                                                                                   |
| OCS    | Occupant Classification System Module  |                                                                                                                                   |
| ABS    | Antilock braking system                |                                                                                                                                   |
| DCDC   | DC to DC Converter Control Module      | Mimics/replaces a traditional alternator, converts power from<br />the traction battery down to the 12-14V for accessory systems. |
| RCM    | Restraint Control Module               |                                                                                                                                   |
| PAM    | Parking Aid Module                     |                                                                                                                                   |
| PSCM   | Power Steering Control Module          |                                                                                                                                   |
| BdyCM  | Body Control Module                    | Brainbox, many subsystems                                                                                                         |
| GWM    | Gateway Module A                       | A router of sorts                                                                                                                 |
| DACMC  | Digital Audio Control Module C         | Audio amplifier/Active noise cancellation system                                                                                  |
| IPMB   | Image Processing Module B              | Backup camera                                                                                                                     |
| FCIM   | Front Controls Interface Module        | Physical radio controls (8-inch touch screen equipped vehicles)                                                                   |
| FCDIM  | Front Control/Display Interface Module | 4-inch non-touch screen/controls on lower trim vehicles                                                                           |
| TCU    | Telematic Control Unit Module          | Cellular modem, either 2g, 3g, 4g (Energi only)                                                                                   |
| PDM    | Passengers Door Control Unit           |                                                                                                                                   |
| DDM    | Drivers Door Module                    |                                                                                                                                   |
| HVAC   | Heating Ventilation Air Conditioning   |                                                                                                                                   |
| RFA    | Remote Function Actuator               |                                                                                                                                   |
| ACM    | Audio Control Module                   | AM/FM/CD/Sirius tuner/audio routing module                                                                                        |
| IPC    | Instrument Panel Control Module        |                                                                                                                                   |
| GPSM   | Global Positioning System Module       |                                                                                                                                   |
| RGTM   | Rear Gate Trunk Module                 |                                                                                                                                   |

## System Information

### Electrical

* [12V Battery](./electrical/low_voltage_battery.md)
