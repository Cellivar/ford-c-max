# Telematics Control Unit - 2G Modem

| Module Property     | Value                              | Notes                                    |
| ------------------- | ---------------------------------- | ---------------------------------------- |
| AsBuilt Module Code | 754                                | Same as the 3G unit                      |
| Part number         | TODO                               | Read the label on the trunk module       |
| Calibration         |                                    |                                          |
| Strategy            | DM5T-14G139-DF                     | Read via UDS DID F188                    |
| Calibration Level   |                                    |                                          |
| Location            | Driver's side panel in trunk       | Same spot as the later modems            |
| Bus                 | MS-CAN                              | Confirmed by UDS sweep, see below        |

The original modem shipped on 2013-2014 model year vehicles. These were rendered useless by the [shutdown of the AT&T 2G network in January 2017](https://www.att.com/att/2g-sunset-timeline.html), which is what prompted the 2016 recall that installed the [3G modems](./TCU_3G.md). Cars that missed the recall still carry these in the trunk as paperweights.

The reference vehicle for this page is a 2014 C-Max Energi (the "2014 Energi Sony" column in the [Central Config comparison](/systems/modules/configs/cc.csv)).

## Strategy Family

The observed strategy `DM5T-14G139-DF` is interesting: the 3G modem's strategy is `HJ5T-14G139-UM` — the _same_ `14G139` telematics application family. The telematics application firmware spans modem generations, and the cellular modem itself is a separate sub-part of the module. Don't assume a different strategy prefix means a totally different brain inside.

## AsBuilt Configuration

Unlike the 3G unit's many blocks, the 2G TCU exposes a single block: `0754-01-01`. From the 2014 Energi this data was gathered from: `7000 0000`, checksum `00CD`.

The 3G unit's bit decode table on the [3G page](./TCU_3G.md) does _not_ apply cleanly to this value (it produces invalid APIM/engine type values), so the 2G block layout appears to be different and remains undocumented. TODO.

## Observed Failure Mode: U3000:04

A 2014 Energi with this modem exhibited the classic dead-telematics symptoms:

* ESN never showed up in MyFord Mobile
* Scheduled "Go Times" never executed (including ones set in the car)
* Timekeeping drifts

A UDS DTC read found exactly one code stored: **U3000:04** — the module reporting an internal system failure of _itself_. Ford uses this same code family on other modules (see SSM45724/SSM45809/SSM46048 for APIMs logging it).

The interesting part is what _didn't_ show up:

* The module's CAN-facing side is healthy: it answers TesterPresent, enters extended diagnostic sessions, and serves identity DIDs cleanly.
* No other module on either bus logged an active "lost communication with TCU" code.

So the fault is internal (modem/provisioning subsystem), not on the network. This matches the symptoms: ESN reporting requires the provisioning state machine to complete, Go Times are executed by the TCU's scheduler (see the schedule-related alerts in the [3G AsBuilt blocks](./TCU_3G.md)), and the TCU served as a time reference for scheduled functions. An internally-failed TCU breaks all three even with a live network.

## UDS Diagnostic Surface

Observed by direct UDS interrogation over MS-CAN (see [OBD adapters](/tools/obd_adapters.md)):

* `3E` TesterPresent: positive
* `10 03` extended diagnostic session: positive (`50 03`)
* `27` SecurityAccess: negative `7F 27 7F` (not supported in active session — exists somewhere, likely behind a programming session)
* `23` ReadMemoryByAddress: negative `7F 23 11` (unsupported outright — no in-car flash reading)
* Identity DIDs: only `F188` (strategy) responds; `F185`/`F186`/`F187`/`F190` (VIN) all return `7F 22 31`

## Source

* Live UDS interrogation of a 2014 C-Max Energi, October 2026
