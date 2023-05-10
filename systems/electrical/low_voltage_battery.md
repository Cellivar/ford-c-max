# Low voltage battery

The C-Max, like all vehicles, has a high voltage and a low voltage system. The low voltage system is managed by a standard lead acid 12v battery located in the trunk.

Batteries die over time. When you get a new replacement battery [you must reset the BMS history](/maintenance/procedures/bms_battery_age_reset.md) or it will misbehave.

You might also be [curious about modern replacements](./low_voltage_battery_alternatives.md) for lead acid, I did some research and came to a conclusion.

## Battery Details

The OEM battery model number is a Motorcraft BXT67R. As of mid-2023 it is $160 direct from Ford, and $210 for the auto part store versions of the same thing.

Some details:

| Name                     | Data       | Notes                                                 |
| ------------------------ | ---------- | ----------------------------------------------------- |
| Cold Cranking Amps (CCA) | 390        | Not that a C-Max cranks..                             |
| Cranking Amps (CA)       | 487.5      |                                                       |
| Reserve Capacity         | 65 minutes |                                                       |
| Length                   | 8 1/4in    |                                                       |
| Width                    | 6 7/8in    |                                                       |
| Height                   | 6 7/8in    | Weirdly short, shorter than most others               |
| Group Size               | 67R        | This is a hard-to-find size, expensive too            |
| Positive terminal        | Right side | Reversed from "standard" batteries!                   |
| Battery Vent Tube        | Yes        | Behind the battery, make sure it's installed.         |
|                          |            |                                                       |
| Ford OEM Cost            | $160       | According to [fordparts.com](https://parts.ford.com/) |
| Part store battery cost  | $210       | Advance, O'Reilly, etc.                               |
|                          |            |                                                       |

As noted, the 67R is a weird battery size that is hard to find. Additionally the weirdly low 390 CCA and 65 minute reserve capacity. What? Why are none of these regular numbers?

### An aside about battery terms

What is a cold cranking amp and what is reserve capacity?

Cold Cranking Amps are somehow an official measurement of battery power delivery. CCA is defined as:

> The number of amps produced by a _fully charged_ battery during a _30 second period_ while maintaining at least _7.2 volts_ at a temperature of 0°F (-18°C)

I come from an electronics background so I'm looking for a C-rating, but that's not how lead acid batteries used to be used in cars. For a car it's all about how much power can that battery push through a starter motor (and nothing else) in the middle of winter to start the car. That's all they care about, therefore that's what batteries are rated at. Lead-acid batteries are built like tanks compared to other chemistries and will happily throw amps at a dead short for as long as they can. Thus, cold cranking amps instead of a C-rating.

What about reserve capacity? Cranking amps tells you dead-short delivery to the starter motor, reserve capacity tells you how long you can leave the lights on. Reserve capacity is defined as:

> The number of _minutes_ a _fully charged_ battery can deliver _25 amps_ while maintaining at least _10.5V_ at a temperature of 80°F (26.5°C).

This gives us the opposite side of the coin: how long can you leave the lights on and the radio blasting until you can't start the car anymore.

### C-Maxes are not ICE vehicles

A C-Max does not have a starter motor nor does it use the 12V system to start the engine at all. The 12V battery is used to energize the main contactors to the high voltage system, brings the DC-DC converter online, and then the DC-DC converter drives the entire vehicle. The HP35 transmission and engine then is all driven off the high voltage.

The 12V system can successfully start the car down to 10.1V, beyond that it starts to get dicey and the car gets progressively more frustrated about actually starting.

KEY TAKEAWAYS:

* The C-Max doesn't actually care about the CCA of the battery.
* Ford chose to use a weird battery size for some reason, probably cost savings, and it sucks.
* If you have a 2013 C-Max with the 12V power drain issue the Reserve Capacity won't save your bacon, carry one of thsoe jump-start power packs.

## Body Control Module Battery Monitoring System

On Ford C-Platform vehicles the Battery Monitoring System is integrated into the Body Control Module. On Forscan all of the related datapoint PIDs will show up as part of the `BdyCM` module.

Lead acid batteries decay over time and lose capacity. The best you can do is slow this down through careful charging and discharging. The purpose of the BMS is to monitor and control the battery to help maximize its lifetime and (attempt to..) prevent coming out to a dead car when you want to drive.

The Ford BMS monitors power _into_ and _out of_ the battery. The BMS sits between the battery's terminals and the overall electrical system. This is partly why it is important to _not_ bypass the BMS and attach accessories directly to the battery lugs, the BMS needs to keep track of the battery capacity to do its job.

Unfortunately for the BMS it can't directly determine the battery health or current charge level, it can only _indirectly_ measure these. It does this using three things: voltage monitoring, coloumb counting, and blind guesswork. This is important because overcharging a lead-acid battery CAN MAKE IT EXPLODE.

The first two checks are easy. Charge the battery to full. Attach a load to it, counting the energy that is extracted, until the voltage drops low. Attach a charger, counting the energy that is input, until the voltage reaches fill again. This is part of what the BMS does and is how the BMS determines the battery has gotten too low. If the BMS thinks the battery is too low it will:

* Make the APIM screen show a "Screen off to save power" message
* Throw DTCs if it's angry enough about it
* Send a "Low 12V Battery" alert to the MyFordMobile / FordPass system
    * Or at least it used to. It's unclear if something is actually listening for these now with the 4G modem upgrade.
* Put the vehicle into "Deep sleep" and disable things like the cellular modem and other "unnecessary" loads.
    * In my 2013 this behavior is rare. I think I've caught my car in deep sleep a handful of times total since I bought it, it otherwise just dies.

Over time lead-acid batteries degrade and lose capacity. Fortunately we've been using them in cars for a century so we have some pretty good data on _how fast_ they degrade. This is built into the BMS as part of the "Battery Days In Service" value. The BMS uses that to guess what kind of capacity the battery _should_ have given its age, and _adjust the charging profile of the battery to compensate_. This helps extend battery life and avoid explosions.

If the BMS thinks your battery is 5 years old it will believe your battery has a reduced capacity to take in power. It will avoid overcharging this older battery because of the aforementioned EXPLODING that overcharged batteries can do. If you replace your battery but don't reset the BMS then it will undercharge your battery until it's barely surviving overnight.

KEY TAKEAWAYS:

* Don't lie to the BMS by bypassing it.
* [Reset the BMS](/maintenance/procedures/bms_battery_age_reset.md) when you get a new battery or you will have a bad time.

Sources:

* [This FordAuthority article](https://fordauthority.com/2022/11/ford-battery-monitoring-system-explained-in-depth-by-technician/)
* [Threasd on the hybrid forum](https://fordcmaxhybridforum.com/topic/7304-computer-reset-after-changing-battery/)
* Ford's Modification Guide publication for the C-Max.
