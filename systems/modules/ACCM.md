# Air Conditioning Control Module

| Module Property     | Value                  | Notes |
| ------------------- | ---------------------- | ----- |
| AsBuilt Module Code | 7C7                    |       |
| Part number         | DG9H-19F611-AB         |       |
| Calibration         |                        |       |
| Strategy            | DG9H-14D491-AB         |       |
| Calibration Level   | DG9H-19F611-AB         |       |
| Location            | Part of A/C compressor |       |
| Bus                 |                        |       |

The ACCM is responsible for managing the compressor and related controls for the air conditioning system. When the HVAC controller commands the compressor to run the ACCM manages the actual running of the compressor.

In C-Max vehicles the ACCM is special as it's managing power draw from the high voltage battery to run the compressor, which can use several kilowatts of power draw if it's running hard. Running the A/C on electric mode can take a serious bite out of your vehicle range as a result.

## AsBuilt Configuration

The ACCM has no AsBuilt configuration.
