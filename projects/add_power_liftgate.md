# Adding the OEM powered liftgate

The [2013 C-Max Equipment Group 302A](/docs/ford/marketing/2013-cmax-brochure.pdf) included a powered liftgate with a foot-activated open feature. The liftcate will power itself open and closed, all the way down to latching firmly in place. A radar sensor under the rear bumper will sense a foot wave and will open the trunk. There is also a button under the HVAC controls to open the trunk from the cabin. My C-Max Energi SEL did not have this feature, and I added it.

## Parts

It turns out the kick sensor and the powered liftgate are entirely independent. You can install one without the other, including just the kick sensor without the powered liftgate.

Parts for the kick sensor:

| Parts                    | Part Number          | Notes                                                  |
| ------------------------ | -------------------- | ------------------------------------------------------ |
| Rear bumper wire harness | FV6Z-15K868-BBA      | With park sensors and powered liftgate                 |
| Upper handsfree sensor   | CJ5Z-14F680-C or -F | Same part number as Escape and others in similar years |
| Lower handsfree sensor   | CJ5Z-14F680-D or -G | Same part number as Escape and others in similar years |
| Handsfree control module | CJ5Z-14B291-C        | Same part number as Escape and others in similar years |
| Bumper cover bracket     | DM5Z-17779-A         | The part sticker says "open sesame bracket"            |

Parts for the powered liftgate:

| Parts                                              | Part Number     | Notes                                                        |
| -------------------------------------------------- | --------------- | ------------------------------------------------------------ |
| Dash autopark switch                               | DM5Z-9C888-B    | 4 button for Energi, I think the Hybrid had a different one? |
| Power liftgate switch rear                         | 1L2T-14K147-AA  | Motorcraft SW-5855, cheap clones are fine                    |
| Power striker motor                                | AM5Z-15790-C    |                                                              |
| Liftgate latch                                     | AM5Z-5843150-D  | Old part was AM5Z-1743150-A                                  |
| Pivot bracket - right                              | AM5Z-28442A38-D | AKA AM5Z-58442A38-B. Re-use the bolts                        |
| Pivot bracket - left                               | AM5Z-58442A38-E | AKI AM5Z-58442A38-A. Re-use the bolts                        |
| Tailgate strut motor - Left                        | AM5Z-58406A11-D | AKA AM5Z-58406A11-B, AM5Z-58406A11-C                         |
| Tailgate strut motor - Right                       | AM5Z-58406A10-F | AKA AM5Z-58406A10-C, AM5Z-58406A10-E                         |
| Liftgate pinch sensor - right                      | AM5Z-58406A76-A |                                                              |
| Liftgate pinch sensor - left                       | AM5Z-58406A77-A |                                                              |
| Liftgate pinch sensor clip                         | AM5Z-14197-A    | 8 total                                                      |
| [Rear Gate Trunk Module](/systems/modules/RGTM.md) | AM5Z-14B291-E   | There was a -A but it's more rare, either works.             |
| Lower power liftgate harness                       | FV6Z-13A409-A   | See note                                                     |
| Upper liftgate harness                             |                 | See note                                                     |

The wire harness for the liftgate is confusing and difficult to fully understand.

## Connectors

TODO!

## Installation

### Kick sensor installation

This one is fairly straightforward, the hardest part is adding pins to the existing plug and running them up into the body of the vehicle.

TODO!

### Powered liftgate installation

TODO!

###

## Configuration

## Notes

The two big concerns I had going into this project were:

* Will it be fast enough to not be annoying?
* Can I operate it manually if it breaks?

The answer to both is a firm "yes". The liftgate can be operated manually (though of course it is harder than the non-powered version). The liftgate operates itself only a little bit slower than a human operating the liftgate, and it can be downright scary if it starts moving down on you in an unexpected way.

I can hit the button on the remote fob while rolling up with a cartload of groceries and be immediately ready to throw them all in by the time I'm at my car. I can open the liftgate at a distance for a friend throwing junk in the car. I can press the button on the center console and have the liftgate wide open by the time I climb out of the car and get there. I can pick up my partner from the airport and open the liftgate for their bags without having to put the vehicle in park.

I have activated the kick sensor more times accidentally in my garage than I have activated it intentionally with stuff in my arms. It's just useful enough that I still don't want to disable it, but it's not the obvious win. This is exacerbated by the way we park in our garage and that my workbench is near the rear of my car's parking spot.
