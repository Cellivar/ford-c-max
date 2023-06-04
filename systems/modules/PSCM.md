# Power Steering Control Module

| Module Property     | Value          | Notes |
| ------------------- | -------------- | ----- |
| AsBuilt Module Code | 730            |       |
| Part number         | CV61-3C579-AD  |       |
| Calibration         | CV6T-14C218-AD |       |
| Strategy            | CV6T-14C217-AD |       |
| Calibration Level   | CV61-3C579-AD  |       |
| Location            | Steering rack  |       |
| Bus                 | HS-CAN         |       |

The PSCM is the controller for the electronic power steering (EPS) rack present in all C-Maxes. The steering wheel is mechanically connected to the same system, so when the Active Park Assist is turning the steering wheel it's using the PSCM to drive the steering.

## AsBuilt Configuration

I don't know what these settings are for and haven't found any guidance online.

| 0730-01-01 | Nibble (hex) | Bit | Effect         | Notes |
| ---------- | ------------ | --- | -------------- | ----- |
|            | 0            | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            | 8            | 1   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
|            |              | 0   |                |       |
| CHECKSUM   | 41           |     | Autocalculated |       |
