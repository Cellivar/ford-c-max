# Remote Function Actuator

| Module Property     | Value          | Notes |
| ------------------- | -------------- | ----- |
| AsBuilt Module Code | 731            |       |
| Part number         | AV6N-19G481-AL |       |
| Calibration         | AV6N-14C105-AJ |       |
| Strategy            | AV6N-14C104-AM |       |
| Calibration Level   | AV6N-19G481-AL |       |
| Location            |                |       |
| Bus                 | MS-CAN         |       |

The RFA manages most of the interactions with the Intelligent Access Key (IAK) 5-button fob. This includes the touch-to-lock/unlock functions of the door handles, the lock/unlock buttons, the alarm signal when the fob is activated, and determining if the key fob is inside the vehicle when you push the start button.

The RFA also particpates in PATS handshakes with the [Body Control Module](BdyCM.md) to determine if the key is the right key. It will also send messages to the IPC to display things like "No key detected" and "Alarm will go off if you don't start the car in 20 seconds".

## AsBuilt Configuration

The RFA has no AsBuilt configuration.
