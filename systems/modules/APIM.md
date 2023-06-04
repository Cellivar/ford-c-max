# Accessory Protocol Interface Module

## Original

TODO!

## Sync 3 Retrofit

| Module Property     | Value                   | Notes |
| ------------------- | ----------------------- | ----- |
| AsBuilt Module Code |                         |       |
| Part number         | CM5T-14F642-AF          |       |
| Calibration         |                         |       |
| Strategy            | CM5T-14F530-AF          |       |
| Calibration Level   | CM5T-14F642-AF          |       |
| Location            | Behind OBD plug on dash |       |
| Bus                 | All!                    |       |

Note: this is not the touchscreen itself, it is the module mounted to the backside of the touchscreen. Even more specifically it is a daughterboard _inside_ the module that is _separate_ from the computer running the Sync 2 or 3 interface. This is why there are separate module calibrations and Sync 3 software versions, it's two separate computers working together.

The APIM communicates with the Sync computer via a dedicated internal channel.

The Sync 2 APIM and Sync 3 APIM are wildly different. See the appropriate page:

* [Sync 2 APIM](./APIM_sync_2.md)
* [Sync 3 APIM](./APIM_sync_3.md)
