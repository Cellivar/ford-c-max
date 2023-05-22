# Secondary OBD Control Module A (PHEV Battery Charger)

| Module Property     | Value                        | Notes |
| ------------------- | ---------------------------- | ----- |
| AsBuilt Module Code | 7E2                          |       |
| Part number         | FM58-10B689-BC               |       |
| Calibration         |                              |       |
| Strategy            | FM58-14F476-BC               |       |
| Calibration Level   | FM58-10B689-BC               |       |
| Location            | Integrated into battery pack |       |
| Bus                 |                              |       |

The SOBDM is a poor name for the High Voltage Battery Charger, the unit responsible for taking the power from the plug and using it to charge the battery. When the vehicle is charging the CAN network is active and a bunch of modules wake up, including this one, to perform the charging process.

The C-Max has a 3.6kW onboard charger capable of charging the vehicle in around an hour and a half at full tilt. The more your battery degrades the faster it will charge, of course.

## AsBuilt Configuration

The SOBDM has no AsBuilt configuration.
