# Passenger's Door Module

| Module Property     | Value            | Notes |
| ------------------- | ---------------- | ----- |
| AsBuilt Module Code | 741              |       |
| Part number         | AV6N-14B533-FC   |       |
| Calibration         | AV6N-14C109-EC   |       |
| Strategy            | AV6N-14C108-AH   |       |
| Calibration Level   | AV6N-14B533-FC   |       |
| Location            | Passenger's door |       |
| Bus                 | MS-CAN           |       |

As the name implies the PDM is responsible for the functions of the passenger's door. This includes the handle, mirror, locks, windows, buttons, switches, etc. Very few of those controls end up going directly into the vehicle, instead they go through the PDM.

The PDM is responsible for learning the window regulator locations after a power cycle. If your windows do not "auto-up" the PDM needs to re-learn the distance calculation. Roll them all the way down, all the way up, all the way down, and all the way up again. This should remove the learning DTC they throw, especially after a 12V power loss like a dead battery.

## AsBuilt Configuration

The PDM has no AsBuilt configuration.
