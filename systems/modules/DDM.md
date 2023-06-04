# Driver's Door Module

| Module Property     | Value          | Notes |
| ------------------- | -------------- | ----- |
| AsBuilt Module Code | 740            |       |
| Part number         | AV6N-14B531-FC |       |
| Calibration         | AV6N-14C065-EC |       |
| Strategy            | AV6N-14C064-AH |       |
| Calibration Level   | AV6N-14B531-FC |       |
| Location            | Driver's door  |       |
| Bus                 | MS-CAN         |       |

As the name implies the DDM is responsible for the functions of the driver's door. This includes the handle, mirror, locks, windows, buttons, switches, etc. Very few of those controls end up going directly into the vehicle, instead they go through the DDM.

The DDM is responsible for learning the window regulator locations after a power cycle. If your windows do not "auto-up" the DDM needs to re-learn the distance calculation. Roll them all the way down, all the way up, all the way down, and all the way up again. This should remove the learning DTC they throw, especially after a 12V power loss like a dead battery.

## AsBuilt Configuration

The DDM has no AsBuilt configuration.
