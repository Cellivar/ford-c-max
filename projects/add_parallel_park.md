# Adding the OEM Active Park Assist

The [2013 C-Max Equipment Group 303A (Parking Technology Package)](/docs/ford/2013-cmax-brochure.pdf) included 2 features: Active Park Assist (APA) and Forward Sensing System (front-mounted PDC sensors). This was a pretty neat feature set for the era, and allows the vehicle to control the steering wheel angle when parallel parking.

In 2020 the planet went into enforced staying at home and I got so bored I figured out what it would take to install this on my car.

## Theory

Ford's Active Park Assist (APA) is the first generation of a set of park assist features that gained additional features over time... in other vehicle models The Fusion, for instance, can not only parallel park, it can also pull into a perpendicular parking spot. It is also capable of driving itself *out* of a tight parking spot, which is impressive and would be useful sometimes for myself. Alas the C-Max only ever had APA as an option.

The APA system integrates multiple modules to make the magic happen

* [APIM](/systems/modules/APIM.md) orchestrates, finding a space and displaying instructions.
* [Parking Aid Module](/systems/modules/PAM.md) for PDC sensor input to determine whether you're about to hit the cars.
* [SASM](/systems/modules/SASM.md) for steering angle sensing.
* [ABS](/systems/modules/ABS.md) for wheel distance travel and brake status.
* [PSCM](/systems/modules/PSCM.md) for steering angle control.
* [ACM](/systems/modules/ACM.md) for beeping at you for instructions.

The Parking Distance Control (PDC) sensors are small ultrasonic sensors that fit into the front and rear bumpers. On Energi C-Maxes the rear PDC was standard, I think some Hybrid trim levels didn't have them at all. These sensors sit in plastic brackets which then fit into specially shaped holes in the bumpers. There are 6 of them in the front bumper and 3 of them in the rear bumper, for a total of 9 around the vehicle.

The two outermost forward PDC sensors on the front bumper face directly out the side of the vehicle, and have a longer sensing distance. The APA system uses these to determine whether a parking space is available. When one is found the system will alert you and start providing instructions, such as rolling forward far enough to start the manouver.

The APA system is always active at low speed (under 20 MPH) searching for parking spaces, which means you can push the button to engage the system even just after having found a spot and the system can still guide you into it.

## Parts

| Part                                          | Part Number       | Notes                                                                      |
| --------------------------------------------- | ----------------- | -------------------------------------------------------------------------- |
| Dash autopark switch                          | DM5Z-9C888-B      | 4 button for Energi, I think the Hybrid had a different one?               |
| Active Park Assist Module (PAM)               | CJ5T-15K866-BH    | The -A series is rear PDC only, does not work with APA. Must be a-B series |
| Front bumper parking aid wiring harness w/fog | FV6Z-15K86-7B     | There are 4 versions this is w/fog, w/park aid sensors                     |
| Autopark Sensor                               | CV6Z-15K859-AAPTM | Get 2. Can't use any other model.                                          |
| Parking Aid Sensor                            | Note 1            | Get 4. See Note 1                                                          |
| Parking Aid Sensor Bracket                    | Note 2            | Get all 6. See Note 2                                                      |
| Rear ABS wheel speed sensor w/autopark        | JV6Z-2C190-B      | Get 2. Motorcraft BRAB-574 may be easier to find.                          |
| PAM Connector C4014A                          | Find used         | The pigtail is way too expensive, find used somewhere                      |
| PAM Connector C4014B                          | Find used         | Same here                                                                  |
| 22 AWG wire                                   | Find online       | See Note 3                                                                 |

My C-Max Energi came with the rear PDC sensors already installed. If yours did not you have extra work to do here, good luck. You will need the rear bumper parking aid wiring harness, you will need to figure out if the wires for the PAM are present (and add them if not), and you may need to special order the gasket to run the wires out the bottom of the trunk area to plug into the rear PDC sensors. You'll also need 3 more regular Parking Aid Sensors.

### Note 1: Parking Aid Sensors

You need 4 of these. Ford made a whole bunch of model numbers for these and they seem to be pretty much interchangable. I ordered mine piecemeal off eBay to try and save some money.

Again, the two for the very edge of the bumper _are a different type and cannot be used_. Do not mix these 4 PDCs with the 2 special APA sensors.

* AM5Z-15K859-AAPTM - 2013 original part number for all 4 (and the 3 rear ones if you don't already have them)
* CJ5Z-15K859-AA and AB, AC, AD, AE, AF, AG, AH, AJ, AL, AM are all supersessions of the original.

### Note 2: Parking Aid Sensor Brackets

You need all 6 of these _and they're all different and unique_. It's crazy. I didn't believe it until I was looking at all 6 in front of me and sure enough, they're all a little different.

From left to right around the front bumper:

* CP9Z-15K861-CAPTM - Far left APA
* DM5Z-15K861-CAPTM - Front outer left PDC
* DM5Z-15K861-DAPTM - Front inner left PDC
* DM5Z-15K861-AAPTM - Front inner right PDC
* DM5Z-15K861-BAPTM - Front outer right PDC
* AM5Z-15K861-CAPTM - Far right APA

For completeness here are the rear bumper ones, skip these if it's already installed.

* AM5Z-15K861-AAPTM - Left PDC
* DM5Z-15K861-AAPTM - Center PDC
* DM5Z-15K861-EAPTM - Right PDC

### Note 3: Wires

This mod involves a ton of wires. Prepare yourself.

IF you order the entire front bumper parking aid wiring harness you can avoid a lot of headache for yourself across the front bumper, especially since there's a lot of connectors for the PDC sensors you'd otherwise have to order individually anyway.

The PAM is located in the far back trunk on the passenger side. The wires need to go from there all the way to the buttons just below the HVAC controls. I don't know precisely how far this was, I just ordered a large spool of wire since I'll use it for other projects.

This is a good time to also run the wires you need for the [power liftgate](./add_power_liftgate.md) since the autopark switch includes the

## Connectors

Connector names are from the 2013 wiring diagram book.

TODO!

## Installation

* Take the front bumper off and apart, then cut out the sensor template holes. Make sure to make it exact, the shape of the hole is how the brackets fit tightly and keep the sensors aligned properly. 

TODO!

### Paint

TODO!

## Configuration

* [Set bidirectional rear ABS sensors in the ABS module](/systems/modules/ABS.md).
* [Set bidirectional rear ABS sensors in the Central Config](/systems/modules/ford_central_config.md).
* [Set parking assistance to APA in the Central Config](/systems/modules/ford_central_config.md).
* [Enable APA in the IPC](/systems/modules/IPC.md).
* [Enable APA in the APIM](/systems/modules/APIM.md).
* [Enable APA in the IPMB](/systems/modules/IPMB.md).

## Notes

This amazes my friends every time I get to try it. I personally don't have a lot of trouble manually parallel parking, so this wasn't a huge win for APA.

It works for parallel parking both on the left and right sides of the street, use your turn signal to switch.

The bigger win is the front PDC boops. The C-Max's really blunt nose can make it difficult to judge when I'm close enough to a tight parking spot or tight garage to squeeze into, and having the PDCs to help guide can help a lot here. Combined with [the rear camera project](./add_oem_camera.md) I feel very confident pulling my car into very tight parking spaces.

One of the downsides to enabling this feature is the Sync display will show you a visual indicator of the front PDC sensors every time you slow down to around 5 MPH. This means every time you stop at a stop light the APIM will display a popup of your car with the sensors. You can tap on the screen behind the popup to dismiss it. It gets very old very fast.
