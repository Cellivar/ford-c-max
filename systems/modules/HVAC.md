# Heating Ventillation Air Conditioning

| Module Property     | Value          | Notes |
| ------------------- | -------------- | ----- |
| AsBuilt Module Code | 733            |       |
| Part number         | DM5T-14F509-AG |       |
| Calibration         | CM5T-18D620-AL |       |
| Strategy            | CM5T-18D619-AL |       |
| Calibration Level   | DM5T-18C612-AH |       |
| Location            |                |       |
| Bus                 |                |       |

The HVAC control module does, as the name implies, control the various air ducts, fans, and temperature senors that make up the internal HVAC system of the vehicle. Most of the components are in the dash somewhere. It communicates with the [FCIM](./FCIM.md)/[FCDIM](./FCDIM.md) and [APIM](./APIM.md) for controls and drives the [ACCM](./ACCM.md) to manage cooling power.

## AsBuild Configuration

I haven't found any notes on this. There is no guidance in FORScan or CyanLab's database.

| 0733-01-01 | Nibble (hex) | Bit | Effect         | Notes |
| ---------- | ------------ | --- | -------------- | ----- |
|            | 0            | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            | 0            | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
| CHECKSUM   | 3C           |     | Autocalculated |       |
