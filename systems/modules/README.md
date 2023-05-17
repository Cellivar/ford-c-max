# Individual Module pages

These pages break out the individual modules of the vehicle with notes about them.

You may want to [start at the top of systems](/systems) or select a specific module:

| Code                          | Name                                   | Description                                                                                                                       |
| ----------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [SOBDMC](./SOBDMC.md) | Secondary OBD Control Module C         | Hybrid/transmission control module                                                                                                |
| [BECM](./BECM.md)     | Battery Energy Control Module          | High voltage, not the 12V                                                                                                         |
| [SOBDM](./SOBDM.md)   | Secondary OBD Control Module A         | Onboard PHEV charger (Energi only)                                                                                                |
| [PCM](./PCM.md)       | Powertrain Control Module              |                                                                                                                                   |
| [OBDII](./OBDII.md)   | On Board Diagnostic II                 |                                                                                                                                   |
| [APIM](./APIM.md)     | Accessory Protocol Interface Module    | The 'head unit' touchscreen/Sync module                                                                                           |
| [ACCM](./ACCM.md)     | Air Conditioning Control Module        |                                                                                                                                   |
| [GFM](./GFM.md)       | Generic Function Module                | Charge port light ring (Energi only)                                                                                              |
| [SASM](./SASM.md)     | Steering Angle Sensor Module           |                                                                                                                                   |
| [OCS](./OCS.md)       | Occupant Classification System Module  |                                                                                                                                   |
| [ABS](./ABS.md)       | Antilock braking system                |                                                                                                                                   |
| [DCDC](./DCDC.md)     | DC to DC Converter Control Module      | Mimics/replaces a traditional alternator, converts power from<br />the traction battery down to the 12-14V for accessory systems. |
| [RCM](./RCM.md)       | Restraint Control Module               |                                                                                                                                   |
| [PAM](./PAM.md)       | Parking Aid Module                     | If equipped with parking distance sensors                                                                                         |
| [PSCM](./PSCM.md)     | Power Steering Control Module          |                                                                                                                                   |
| [BdyCM](./BdyCM.md)   | Body Control Module                    | Brainbox, many subsystems                                                                                                         |
| [GWM](./GWM.md)       | Gateway Module A                       | A router of sorts                                                                                                                 |
| [DACMC](./DACMC.md)   | Digital Audio Control Module C         | Audio amplifier/Active noise cancellation system                                                                                  |
| [IPMB](./IPMB.md)     | Image Processing Module B              | Backup camera, if equipped                                                                                                        |
| [FCIM](./FCIM.md)     | Front Controls Interface Module        | Physical radio controls (8-inch touch screen equipped vehicles)                                                                   |
| [FCDIM](./FCDIM.md)   | Front Control/Display Interface Module | 4-inch non-touch screen/controls on lower trim vehicles                                                                           |
| [TCU](./TCU.md)       | Telematic Control Unit Module          | Cellular modem, either 2g, 3g, 4g (Energi only)                                                                                   |
| [PDM](./PDM.md)       | Passengers Door Control Unit           |                                                                                                                                   |
| [DDM](./DDM.md)       | Drivers Door Module                    |                                                                                                                                   |
| [HVAC](./HVAC.md)     | Heating Ventilation Air Conditioning   |                                                                                                                                   |
| [RFA](./RFA.md)       | Remote Function Actuator               |                                                                                                                                   |
| [ACM](./ACM.md)       | Audio Control Module                   | AM/FM/CD/Sirius tuner/audio routing module                                                                                        |
| [IPC](./IPC.md)       | Instrument Panel Control Module        |                                                                                                                                   |
| [GPSM](./GPSM.md)     | Global Positioning System Module       |                                                                                                                                   |
| [RGTM](./RGTM.md)     | Rear Gate Trunk Module                 | Powered liftgate controller, if equipped                                                                                          |

## Reading AsBuilt Config tables in these docs

I record the AsBuilt data as a series of bits, as that's really how it's interpreted by the module firmware. For ease of reading I also include the Nibble that each 4 bits combines to. For example the GPSM module has a config table that looks like this:

| 0701-01-01 | Nibble (hex) | Bit | Effect         | Notes |
| ---------- | ------------ | --- | -------------- | ----- |
|            | 2            | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 1   |                |       |
|            |              | 0   |                |       |
|            | 0            | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
| CHECKSUM   | 2A           |     | Autocalculated |       |

Reading top-to-bottom in the nibble column gets us what we see in FORScan from left to right, so FORScan should show us `701-01-01` as `202A`.

If you wanted to modify that value you would line up the bits in the same order and convert from bits to nibbles (in hex). Let's say we wanted to modify bit 4 in the table from 0 to 1. We would line up those four bits as `0011` and convert to hex `3` for our new nibble value. We line up the new nibbles in order to get `302A` for our FORScan input. Since we changed something the checksum value is wrong, but we can let FORScan figure out the correct value automatically.
