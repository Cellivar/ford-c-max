# Adding the OEM Rear View Camera

## Parts

| Parts          | Part Number    | Notes                                      |
| -------------- | -------------- | ------------------------------------------ |
| Camera         | DM5Z-19G490-A or -B  | See notes below                            |
| Camera Bracket | BM5Z-19H421-A  | Holds the camera in the liftgate handle    |
| Camera Pigtail | WPT-1280       | 2013 wiring diagrams show wrong connector! |
| IPMB           | CM5T-19H423-AB |                                            |
| IPMB Pigtail   | WPT-998        |                                            |
| Add-a-fuse kit | Find online    | Needed for pin 4 of IPMB for power         |
| 22 gauge wire  | Find online    |                                            |

### Camera Selection

I have a 2013-era camera and a 2017-era camera. The 2017 era camera will turn on and display video, but only the 2013-era camera will also display the backup guide lines and the turn guidelines when steering while backing up. Based on observing the LIN bus traffic the 2013 IPMB is sending messages to the 2017 camera that are just being ignored. Trying to flip IPMB configuration settings to make it work didn't seem to change anything. I suspect the 2016+ cameras use a different LIN address that the 2013-2015 IPMB doesn't know to talk to. More research necessary.

![image](https://github.com/Cellivar/ford-c-max/assets/1441553/0a4799bd-3cdf-46fd-853a-3f928a83af5e)

Even with an OEM 2013 camera my zoom doesn't work `:(`

Some suggestions:

* DM5Z-19G490-A and DM5Z-19G490-B are both valid part numbers, don't know what the difference is.
* If you have a 2013-2015 vehicle use a 2013-2015 camera
* If you have a 2016 or later vehicle use a 2016 or later camera
* Third-party camera modules seem to not talk to anything, so expect only video, no guidelines or anything.

## Connectors

Connector names are from the 2013 wiring diagram book.

The liftgate wiring harness is supposed to have all of these wires present, but the version of the harness installed in vehicles without the RVC and without the powered liftgate omit these entirely. I did not bother trying to find the right liftgate harness as it was too expensive, I just ran the wires to a connector in the driver side D pillar, then from there to the inside of the car.

### C4402 - IPMB Connector

* Diagram callout C4402
* Pigtail part number WPT-998

Fuse 99 is empty and the pin is missing, so you will need to use an Add-A-Fuse kit. I used one of the fuses in the trunk fusebox.

Eventually when I did the [powered liftgate add project](./add_powered_liftgate.md) I purchased a used Escape rear fusebox, took it apart, used the fuse pins out of it to add the correct fuse pins for my fusebox, and was able to wire in [Fuse 31 correctly](/systems/electrical/fuses.md).

Make sure to use twisted pair for the MS-CAN bus otherwise the bus may become unstable and cause problems for your car.

| Pin | Circuit | Circuit Function                                  |
| :-- | :------ | :------------------------------------------------ |
| 1   | GD135   | GROUND - COWL SIDE/PILLAR A LEFT # 3RD POINT 6L2T |
| 2   | VDB06   | CONNECTOR - DIAG # CAN BUS MEDIUM SPEED HIGH      |
| 3   | VDB07   | CONNECTOR - DIAG # CAN BUS MEDIUM SPEED LOW       |
| 4   | CBR99   | FUSE - 99                                         |
| 5   | GM100   | CAMERA GROUND                                     |
| 6   | VMP35   | CAMERA LIN                                        |
| 7   |         | NOT USED                                          |
| 8   | CMP10   | CAMERA POWER                                      |

### C4357 - Camera connector

* Diagram callout C4357
* Pigtail part number WPT-1280

⚠️ The 2013 wiring diagram shows the _wrong_ connector! Do not be fooled!

I didn't use a shielded coax cable because I didn't have one handy, I used a regular very long coax cable with RCA connectors on the ends, using the center wire of the coax for VMP31 and the shield of the coax for RMP31. My image quality is fine.

| Pin | Circuit | Circuit Function |
| :-- | :------ | :--------------- |
| 1   | CMP10   | CAMERA POWER     |
| 2   | VMP35   | CAMERA LIN       |
| 3   | RMP31   | RVC VIDEO RETURN |
| 4   | VMP31   | RVC VIDEO SIGNAL |
| 5   | GM100   | CAMERA GROUND    |
| 6   | DMP31*  | RVC VIDEO SHIELD |

### C2383 - APIM Connector

* Diagram callout C2383
* Unknown part number

You may need to add the pins into the connector if they're missing, good luck! You might see if you can find an adapter or something online, searching eBay for prewired APIM camera harnesses.

| Pin | Circuit | Circuit Function                             |
| :-- | :------ | :------------------------------------------- |
| 14  | VMP31   | RVC VIDEO SIGNAL                             |
| 15  | RMP31   | RVC VIDEO RETURN                             |
| 16  | VDB06   | CONNECTOR - DIAG # CAN BUS MEDIUM SPEED HIGH |
| 17  | VDB07   | CONNECTOR - DIAG # CAN BUS MEDIUM SPEED LOW  |

## Installation

If you don't get a new liftgate handle you will need to cut the hole yourself. There is an outline on the inside of the handle, cut right up to the outline but do not cut it out. Take it slow, I was able to do it with basic garage tools and ended up with a good look and a snug fit that does not rattle. The camera bracket should seat tightly into it without stressing either plastic part. Do not use excessive force, the camera bracket isn't super sturdy.

![image](https://github.com/Cellivar/ford-c-max/assets/1441553/d1a4ba09-7298-427f-a70d-75dee26ca9ed)

![image](https://github.com/Cellivar/ford-c-max/assets/1441553/c736c1a5-f37f-4c0e-914d-947f5f434177)


My 2013 was not wired with the necessary wires in the main wiring harnesses (14041, 14014) so I needed to run twisted pair the whole way from the trunk up to the dashboard.

You'll need twisted pair wire for the IPMB and two shielded conductors for the video signal. I used some coax I had lying around and it's been working fine.

Energi models have the IPMB on the passenger side, but that requires removing the traction battery cooling fan. Instead I added velcro to the RFA module and stuck it on the driver side and ran the wires from there.

Note that the tailgate wire harness will also lack all of the appropriate connectors too, so the wires you choose to run to the camera should be flexible to withstand the liftgate opening and closing. The wire pass-through is fairly crowded, be patient.

## Configuration

* [Configure the IPMB](/systems/modules/IPMB.md).
* [Enable the RVC in the Central Config](/systems/modules/central_config.md).
* [Enable the RVC in the IPC](/systems/modules/IPC.md).
* [Enable the RVC settings in the APIM](/systems/modules/APIM.md).

## Notes

Incredibly useful mod, highly recommend it.
