# Antilock Brake System Module

| Module Property     | Value                        | Notes |
| ------------------- | ---------------------------- | ----- |
| AsBuilt Module Code | 760                          |       |
| Part number         | FV68-2C219-AJ                |       |
| Calibration         |                              |       |
| Strategy            | FV68-2D053-CB                |       |
| Calibration Level   | FV68-2C219-AJ                |       |
| Location            | Engine bay, against firewall |       |
| Bus                 | HSCAN                        |       |

The ABS module is mounted directly to the ABS brake controller and part of the overall braking system. It manages the anti-lock brakes, traction control, hill-hold assist, and is used as part of the brake bleed procedure.

The module is also at least partially responsible for control signals as part of the parallel park aid system, and requires some configuration as [part of parallel park installation](/projects/add_parallel_park.md).

On Fusion vehicles the ABS module participates in the adaptive cruise control, and requires a special hardware version to enable stop-start features. Unfortunately the CGEA architecture of those vehicles makes it unlikely to be able to graft onto a C-Max. Adaptive cruise control is one of the features I really wish I could add to my car.

## AsBuilt Configuration

Most of these values are not documented, and the Cyanlabs listing is only for the CGEA versions of these modules so doesn't line up.

Block 0760-01-01 is the VIN for the vehicle, [see the doc for that.](../ford_vin.md).

| 0760-02-01 | Nibble (hex) | Bit | Effect                            | Notes                       |
| ---------- | ------------ | --- | --------------------------------- | --------------------------- |
|            | 4            | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   | Something to do with FHEV vs PHEV | 0 = PHEV (Energi), 1 = FHEV |
|            |              | 0   |                                   |                             |
|            | 4            | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 1            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 1            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 2            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 1            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 1            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 3            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 0            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 8            | 1   | Rear ABS wheel sensor type        | Note 1                      |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
| CHECKSUM   | FB           |     | Autocalculated                    |                             |
| 0760-02-02 | Nibble (hex) | Bit | Effect                            | Notes                       |
| ---------- | ------------ | --- | --------------------------------- | --------------------------- |
|            | 8            | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 2            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 0            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 0            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 0            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            | 0            | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 0   |                                   |                             |
| CHECKSUM   | ED           |     | Autocalculated                    |                             |
| 0760-03-01 | Nibble (hex) | Bit | Effect                            | Notes                       |
| ---------- | ------------ | --- | --------------------------------- | --------------------------- |
|            | 5            | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            | 5            | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
|            |              | 0   |                                   |                             |
|            |              | 1   |                                   |                             |
| CHECKSUM   | C0           |     | Autocalculated                    |                             |

### Note 1: ABS Sensor Type

As part of my autopark installation I needed to replace the rear wheel ABS sensor type. The C-Max used two types of the sensors.

* 0: Unidirectional sensor
* 1: Bidirectional sensor

The bidirectional sensor is used as [part of the autopark system](/projects/add_parallel_park.md) to calculate how far backwards the vehicle has rolled while parallel parking.

This setting must match the actual installed sensors. If they don't match a DTC will be thrown, the park assist system will _completely_ shut off, the ABS system will throw a fit, and the vehicle may even put itself into limp mode.

Make sure you order the right part when replacing these sensors!
