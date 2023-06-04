# Global Positioning System Module

| Module Property     | Value                  | Notes |
| ------------------- | ---------------------- | ----- |
| AsBuilt Module Code | 701                    |       |
| Part number         | DE8T-19H463-AC         |       |
| Calibration         | DE8T-19H463-AE         |       |
| Strategy            | DE8T-14F055-AE         |       |
| Calibration Level   | DE8T-19H463-AC         |       |
| Location            | Behind IPC, under dash |       |
| Bus                 | MS-CAN                 |       |

The GPSM module is present on 2013-2015 model year vehicles prior to [the Sync 3 APIM transition](/systems/modules/APIM_SYNC3.md). This module is located behind the IPC under the dash for a good view of the overhead sky.

On a [Sync 2 system](/systems/modules/APIM_SYNC2.md) this provided GPS information to the [IPS](/systems/modules/IPC.md), the  and the APIM for turn-by-turn, emergency call location, compass heading, and other software integrations. After [a Sync 3 retrofit](/mods/sync_3_retrofit.md) the module is still used by the old IPC for the compass display.

## AsBuilt Configuration

I don't know what these settings are for and haven't found any guidance online.

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
