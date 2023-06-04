# Generic Function Module (Light Ring Controller)

| Module Property     | Value                  | Notes |
| ------------------- | ---------------------- | ----- |
| AsBuilt Module Code | 7A1                    |       |
| Part number         | CM5T-10C714-BA         |       |
| Calibration         |                        |       |
| Strategy            |                        |       |
| Calibration Level   | CM5T-10C714-BA         |       |
| Location            | Attached to light ring |       |
| Bus                 | HS-CAN                 |       |

The GFM is an obscurely named module that is actually the Charge Port Light Ring Controller. It's responsible for making the pretty glowy lights when your car is plugged in and charging.

The GFM is only present on Energi vehicles and the Ford Focus Electric. Ford did not continue to use the light ring for the new Escape PHEV.

## AsBuilt Configuration

The GFM has no AsBuilt config.

The GFM does take some degree of commands from the APIM, as the light ring settings can be set from the settings panel in the Sync 3 interface. On my retrofitted Sync 3 unit the GFM throws a DTC about invalid data received from the APIM, likely because my GFM was not designed to talk to Sync 3. A firmware update has not helped it. The DTC doesn't seem to cause issues so I generally ignore it.
