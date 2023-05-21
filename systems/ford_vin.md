# Ford Vehicle Identification Numbers

The VIN is, as the name implies, a number that uniquely identifies your vehicle. C-Maxes have them (for obvious reasons).

Vehicle modules sometimes encode the VIN into AsBuilt configurations.

Generally you should avoid sharing your VIN online for the usual reasons that VINs can be used to find more information about someone and/or harass them.

## C-Max VINs

In the modern era Ford VINs are 17 digits long and consist of alphanumeric characters. All C-Max VINs follow a common pattern that reveals information about them.

Ford publishes [VIN Guides](https://www.fleet.ford.com/parts-service/resources/vin-guides/) which you can use to figure out what a VIN means for a particular model year.

This is an example VIN from a wrecked C-Max being parted out on eBay: `1FADP5BU9DL512005`. We'll use that as an example to pick apart.

| Digit | Example  | Note                                                                                                          |
| ----- | -------- | ------------------------------------------------------------------------------------------------------------- |
| 1-3   | `1FA`    | Ford North America, Passenger Car. Same for all C-Maxes.                                                      |
| 4     | `D`      | See note. Restraint and brake type, and GVWR Class. Same for all C-Maxes.                                     |
| 5-7   | `P5B`    | See note. Line, series, body type.                                                                            |
| 8     | `U`      | 2.0L Atkinson iVCT HEV Engine, 188HP. Same for all C-Maxes.                                                   |
| 9     | `9`      | Check digit                                                                                                   |
| 10    | `D`      | See note. Model year.                                                                                         |
| 11    | `L`      | [Wayne, Michigan Assembly Plant](https://en.wikipedia.org/wiki/Michigan_Assembly_Plant). Same for all C-Maxes |
| 12-17 | `512005` | Serial number.                                                                                                |

### Digit 4: Restraint, brake, GVWR rating

Ford uses digit 4 in a lookup table for a few pieces of information that apply to their other vehicle types like trucks and busses. Passenger cars mostly throw that out because they're small and all use hydralic brakes.

All C-Maxes have digit `D` here:

* Hydraulic brakes
* N/A for the GVWR class (like all passenger cars )
* Manual belts with driver and passenger frontal air bags and side inflatable restraint (1st & 2nd row) and
driver knee restraints (air bag)

They changed the 'Restraint Category Number' listing partway through the 2013-2018 range, the actual installed restraints never changed.

### Digit 5-7: Line, series, body type

The first two digits, `P5`, are the same for all C-Maxes. The third digit is what identifies the model type.

* `P5A` - C-Max Hybrid SE
* `P5B` - C-Max Hybrid SEL
* `P5D` - C-Max Hybrid Titanium
* `P5E` - C-Max Energi SE
* `P5C` - C-Max Energi Premium SEL (2013 is just "Premium", 2014+ is "Premium SEL")
* `P5F` - C-Max Energi Titanium

The Fusion had a similar map.

* `P0U` - Fusion Hybrid S
* `P0L` - Fusion Hybrid SE
* `P0R` - Fusion Hybrid Titanium/Platinum
* `P0P` - Fusion Energi SE
* `P0S` - Fusion Energi Titanium/Platinum

The Focus Electric only ever had `P3R`.

### Digit 10: Model Year

* D: 2013
* E: 2014
* F: 2015
* G: 2016
* H: 2017
* J: 2018
* K: 2019 (If only..)

We skip `I` because everyone hates `I` in alphanumeric codes.

### Digit 12-17: Serial number

Ford uses `100001` through `599999` for Ford vehicles and higher number for Lincoln vehicles. The 2013 C-Max straddles the 51-53 series and the 10-11 series. These values don't seem to be strictly sequential, I've observed 2015s and 2017s starting with `11` and and 2018 with `10`. Doesn't line up with FHEV/PHEV differences either.

Thus, generally, this number doesn't hide anything interesting other than your vehicle's unique ID.

## AsBuilt Configuration Format

Ford distributes the vehicle VIN through several modules in the vehicle. These include

* [ABS](./ABS.md)
* [RCM](./RCM.md)
* Probably the [PCM](./PCM.md) somewhere

If you don't want to share your vehicle's VIN be sure to not share the VIN blocks of these modules.

Each VIN is 17 digits long, each digit takes up one byte, so this will be spread across 4 lines in 1 block. We will continue using the same wrecked C-Max `1FADP5BU9DL512005` for this example.

Take each digit individually and [convert to ASCII](https://www.google.com/search?q=convert+to+ascii). So `1 F A` becomes `49 70 65`.

Each ASCII code is then converted from its decimal value to hex, so `49 70 65` becomes `31 46 41`.

Spread that across the block's lines, add a checksum at the end, and you've got the VIN for the module. Here's the ABS module for that wrecked C-Max.

| Block     | Value          |
| --------- | -------------- |
| 760-01-01 | 3146 4144 50B5 |
| 760-01-02 | 3542 5539 44B3 |
| 760-01-03 | 4C35 3132 307F |
| 760-01-04 | 3035 D1        |
