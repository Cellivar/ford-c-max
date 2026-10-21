# Gateway Module A

| Module Property     | Value                   | Notes                                        |
| ------------------- | ----------------------- | -------------------------------------------- |
| AsBuilt Module Code | 716                     | Confirmed by live UDS identification         |
| Part number         | CM5T-14F642-AF          |                                              |
| Calibration         |                         |                                              |
| Strategy            | CM5T-14F530-AF          | A 2014 Energi reported CM5T-14F530-AH via UDS DID F188 — same family, later revision |
| Calibration Level   | CM5T-14F642-AF          |                                              |
| Location            | Behind OBD plug on dash |                                              |
| Bus                 | All!                    |                                              |

## AsBuilt Configuration

The GWM exposes a large set of blocks: `0716-01-01` through `0716-14-01` (fourteen blocks!) in the Motorcraft AsBuilt export. Content of these blocks is currently undocumented. TODO!

The module is alive and answers UDS requests (TesterPresent, extended diagnostic sessions, identity DIDs) directly on HS-CAN from the OBD port, which is convenient given it lives right behind the plug.

