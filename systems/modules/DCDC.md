# DC to DC Converter

| Module Property     | Value                        | Notes |
| ------------------- | ---------------------------- | ----- |
| AsBuilt Module Code | 746                          |       |
| Part number         | FM58-14B227-AF               |       |
| Calibration         |                              |       |
| Strategy            | FM58-14D459-AH               |       |
| Calibration Level   | FM58-14B227-AF               |       |
| Location            | Integrated into battery pack |       |
| Bus                 | HS-CAN                       |       |

The DC/DC convert replaces the traditional alternator in ICE vehicles. The C-Max doesn't have an alternator, it has [two motor/generators that can either drive the vehicle forward or generate power](https://www.youtube.com/watch?v=MZf_BUuW5Qg) depending on what the vehicle is doing.

Instead of an alternator the Ford hybrids have a module that steps down the high voltage power to 12V and supplies that power to the rest of the vehicle.

[Weber Auto has an excellent video walking through how the Ford Hybrid systems work here](https://www.youtube.com/watch?v=kmDpNr1PdMk).

The DC/DC converter is, according to the Ford shop manual, capable of supplying "up to 145 amps" to the 12V system. Under normal conditions with a well charged 12V battery a C-Max turned on in park with DRLs active is approximately 35 amps of power draw on this system. This system powers the 12v outlets, the 150w inverter in the second row (if equipped), and things like fog lights. Turning the lights to 'off', turning off the radio and any interior lights, and removing anything plugged into any 12V outlets would mean approximately 100W of available power on the 12V system for an aftermarket power inverter.

[The user cr08 explored this idea in this thread](https://fordcmaxhybridforum.com/topic/12663-power-inverter-installationoptions/) with some observations about how to wire it into the system. It's something I'd like to explore on my vehicle the next time I go digging around in the trunk area.

## AsBuilt Configuration

The DCDC has no AsBuilt configuration.
