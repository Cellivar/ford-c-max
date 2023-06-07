# Ford Part Number Format

⚠️ For this discussion we are ignoring that Ford made vehicles before the year 1999.

Ford part numbers follow a consistent format that helps identify some details about the particular part. You can use this information to look for similar parts, later-model-year parts, or fill in information gaps.

Part numbers are assigned to a part _when that part is introduced for use_. This means a part that is not changed for the history of a vehicle model will retain the same part number from _the first model year_ to the _final model year_.

## Part Number Structure

Ford part numbers are generally of the format {PREFIX}-{PARTCODE}-{REVISION}, such as `CJ5T-15K866-BH` for my [Parking Aid Module w/APA](/systems/modules/PAM.md).

* The prefix is `CJ5T`
* The base part number is `15K866`
* The revision code is `BH`

Prefix are nearly always a 4-character code in order:

* `C` - Year code
* `J5` - Product Line Code
* `T` - Design Responsibility Code

### Year Code

This is an incrementing alphanumeric value based on the model year of the part's introduction.

* 8 - 2008
* 9 - 2009
* A - 2010
* B - 2011
* C - 2012
* D - 2013
* E - 2014
* F - 2015
* G - 2016
* H - 2017
* J - 2018
* K - 2019

..etc

### Product Line Code

The C-Max internal code name was C344, and was given the product line codes `M5` (shared with the 1st C-Max, 2nd gen C-Max, 2nd gen Focus, 3rd gen Focus), `1C`, and `1D`. In theory these values map to a particular vehicle line that the product was designed for.

The problem with this format is that Ford started interchanging parts across _nearly all_ of their product lines. C-Max parts vary _wildly_ in what these values are and what vehicle line the parts were originally designed for. The door modules use `V6`, which was the C1 platform, which includes many lines of vehicles. It's hard to glean particularly useful information from these values. Nonetheless, here's the full listing I could find.

<details></summary>List of product line codes</summary>

* 11 – Advance Technology
* 1B – B/Car FOE
* 1C – C344
* 1D – C344 C1 Platform
* 1E – C346
* 1F – C346 C1 Platform
* 1G – CD539E/CD390 Platform
* 1H – Ford Millennial
* 1J – JMC Heavy Truck
* 1K – C484
* 1L – B500 Super B
* 1M – CDC Platform
* 1N – Lincoln MPU
* 2B – B-Car FNA
* 2G – CD539N/U540/CD539C
* 3B – B-Car FSAO
* 3G – D544/D568/PLATFORM
* 4B – B-Car (India)
* 5B – B-Car (China)
* 6B – B-Car (Asia)
* 7B – B552
* 81 – PHK 131 LT
* 99 – Ford Motorsports
* A1 – U89-U540
* A2 – Explorer/Sport Trac
* A3 – B376 DS/B2 4DR Notch
* A4 – D401 Mercury Freestyle
* A5 – D385 Lincoln Sedan MKS (2009-2016)
* A6 – B299/B479 Fiesta
* A7 – B450 B-SUV
* A8 – D471 Ford X/Dvr Uty Flex
* A9 – B474 Maverick
* B1 – E385 Lincoln Sedan
* B2 – W414 Ford
* B3 – P376/U375 Pickup
* B4 – J61/J64 Mazda
* B5 – U502 Explorer
* B6 – CD524 Ford Sport Back
* B7 – M526 Lincoln Sport Convertible
* B8 – D257 Lincoln MKS
* B9 – D257 Lincoln MKS-L
* C1 – Transit
* C2 – Econoline
* C3 – F250 Super Duty/350/450/550
* C4 – F650/750/Cargo
* C5 – Aviator
* C6 – CAL 1 Blackwood
* C7 – Excursion
* C8 – U260
* C9 – U297
* CP – Community Plan
* D1 – U469
* D2 – VH280 Aston Martin
* D3 – VH300 Aston Martin
* D4 – VH400 Aston Martin
* D5 – V475 B Panel Van
* D6 – J88 Mazda
* D7 – V196 Econo Van
* D8 – C420
* D9 – D544 Lincoln MKS
* E1 – Not Used
* E2 – C264
* E3 – A29 Think Neighbor
* E4 – A306 Think City
* E5 – CD338 Ford Fusion (2006-2012)
* E6 – Mercury Escape-Mariner (2004-2010)
* E7 – Cab Over Engine Class 5
* E8 – B409 Car
* E9 – D472 Mercury X Over Utility MKT
* F1 – Taurus
* F2 – Windstar Freestar Monteray (F/M)
* F3 – Continental (FWD)
* F4 – Sable (1999-2002)
* F5 – Villager (1999-2002)
* F6 – Volvo
* F7 – Transit
* F8 – FW178
* F9 – 219 Ford Freestyle Taurus X Sable
* G1 – D250 REPLS 500 Taurus
* G2 – U263 Lincoln
* G3 – AM305F Aston Martin
* G4 – AM803 Aston Martin
* G5 – D310 UNC Sport
* G6 – D365 Lincoln CTU
* G7 – Ford GT
* G8 – F237 Lincoln CVT
* G9 – Euco Platform
* H1 – L318/L317
* H2 – L318/L319 TBE1
* H3 – L320
* H4 – L321/L322 TBE2 TBE3
* H5 – L314/L315/L359
* H6 – CD378 Lincoln Zephur MKZ
* H7 – F Series Sports Cab
* H8 – E396 Ford Mercury
* H9 – Not Used
* HC – Harness CompJLR
* J1 – Y465 Volvo
* J2 – Y466 Volvo
* J3 – L513
* J4 – L486 Land Rover 4XX
* J5 – C520 Ford Escape
* J6 – C520/C482 Escape HEV
* J7 – C521/C499/C483 Lincoln SUV
* J8 – Electric C-Car Top Hat
* J9 – Electric C-CAR Platform
* K1 – D568 Taurus (China)
* K2 – V362 Artisan 1 Ton
* K3 – V363 Trunker 2 Ton
* K4 – V363N Trunker 2 Ton
* K5 – L405 JLR Range Rover
* K6 – L494 JLR Range Rover Sport
* K7 – L550 JLR Freelander
* K8 – Troller
* K9 – Not Used
* L1 – Expedition
* L2 – Explorer
* L3 – F150/F250
* L4 – Maverick 4X4
* L5 – Ranger
* L6 – Aerostar
* L7 – Navigator
* L8 – Ford Escape (2000-2012)
* L9 – Mountaineer (1999-2010)
* M1 – Tracer
* M2 – VX62/V191/CD340 Gal
* M3 – J97 Courier
* M4 – J71
* M5 – C214/C307/C344/C346
* M6 – U293 Mazda ELC
* M7 – J37 Mazda GN
* M8 – J56J Mazda
* M9 – U467 3 Raw Product
* N1 – BV226/B515 Eco Sport
* N2 – C195 LKON
* N3 – SE161 Puma
* N4 – S272 (C1)
* N5 – P1 Volvo (C1)
* N6 – J46 Mazda (C1)
* N7 – CD334 Mercury Milan (2006-2011)
* N8 – Not Used
* N9 – CD379/390
* P1 – U470
* P2 – J73 Mazda
* P3 – B2EH Platform Mazda
* P4 – C505 2009 SUV
* P5 – CD533 Lincoln MKZ
* P6 – D532 Taurus B11 Platform
* P7 – 5530 Mustang D11 Platform
* P8 – CD548 Mercury Milan
* P9 – Mercury Focus
* PL – JLR PLA Platform
* R1 – AMV03 Aston Martin
* R2 – Falcon
* R3 – Mustang
* R4 – Scorpio
* R5 – Fairlane
* R6 – LTD
* R7 – E265 Raptor
* R8 – X200 Jaguar
* R9 – Lincoln Mark VIII
* S1 – Aspire
* S2 – Contour (1999-2000)
* S3 – C212 Maverick
* S4 – CE14/C170 ESC Focus
* S5 – BE146/B420/421 Ka
* S6 – BE91/B226/256/Fiesta
* S7 – CD132/162/345/391 Mondeo
* S8 – Probe
* S9 – Mystique (1999-2000)
* T1 – V227 Transit Connect
* T2 – U204 Mazda Unique
* T3 – U293
* T4 – U334/367/CD539
* T8 – J44 Mazda
* T9 – Volva SPA Platform
* U1 – Power Products
* U2 – Motorcraft Brand
* U3 – Outside Sales
* U4 – FEO VEH
* U5 – Ford
* U6 – Global Aftermarket
* U7 – Service Only
* U8 – Castings and Forgings
* U9 – Motorhome
* V1 – B232 BMAV EU FAP
* V2 – B2E Platform Ford
* V3 – B410 TRK
* V4 – C394/C520 C482 Kuga
* V5 – BE2 Platform Mazda
* V6 – C1 Platform
* V7 – J26E Mazda Pickup
* V8 – P501 F100 Pickup 2011
* V9 – P525 F100 Pickup 2012
* W1 – Town Car
* W2 – Cougar
* W3 – Grand Marquis
* W4 – F236 Lincoln LS (1999-2006)
* W5 – EW171
* W6 – Thunderbird RWD (2002-2005)
* W7 – Crown Victoria
* W8 – X100 X150 Jaguar
* W9 – X300/X350/X351/X360
* X1 – X600 Jaguar
* X2 – X250/X260 Jaguar
* X3 – Not Used
* X4 – X400 Jaguar
* X5 – X12 Sports
* X6 – C2 Platform
* X7 – C519
* X8 – C488
* X9 – H492/H566
* Y1 – B2EH Platform Ford
* Y2 – P298 Aston Martin
* Y3 – B516
* Y4 – N352 JMC
* Y5 – VH5 Aston Martin
* Y6 – VH6 Aston Martin
* Y7 – Aston Martin Juliette
* Y8 – P289 Aston Martin
* Y9 – Aston Martin Paris

</details>

### Design Responsibility Code

Similar to the Product Line Code, Ford's strong push to re-use designs means the team responsible for the design of a part can be hard to trace. Sometimes though it can provide interesting meaning, such as The DC/DC converter has part number `FM58-14B227-AF`. The 8 in the prefix indicates it came from the Electric Vehicle Engineering group.

Notable codes:

* T - Electrical Research & Vehicle Tech Ops
* 8 - Electric Vehicle Engineering
* U - Electric and Fuel Handling Operations

<details></summary>List of design responsibility codes</summary>

* A – Light Truck Engineering Division
* B – Body and Electrical Product Division
* C – Chassis Operations
* D – Overseas Product Engineering
* E – North American Engine Engineering
* F – Electrical and Electronics Division
* G – Engine Mechanical Operations
* H – Climate Control Operations
* J – Customer Srvc Div Parts & Acc Engineering
* K – Import Release Section
* L – Customer Service Div Power Products
* M – Performance/Special Vehicle Operations
* N – Volvo
* O – Outside
* P – Auto Trans &Transaxle Manu Engineering
* Q – Diesel Engine Operations
* R – Manual Trans & Transaxle Manu Engr
* S – Light & Heavy Truck Special Order Parts
* T – Electrical Research & Vehicle Tech Ops
* U – Electric and Fuel Handling Operations
* V – Domestic Special Order Engineering
* W – Axle and Driveline Engineering
* X – Plastic and Trim Products Operations
* Y – Special Vehicle Vehicle Center 1
* Z – Ford Customer Service Department
* 1 – European PD Center
* 2 – Land Rover Vehicle Center
* 3 – Large Luxury Vehicle Center
* 4 – Truck Vehicle Center
* 5 – Ford South American Operations
* 6 – Ford Otosan (Turkey)
* 7 – Transmission and Axle Engineering
* 8 – Electric Vehicle Engineering
* 9 – Australia Asia Pacific Center

</details>

## Part Code

The middle part of a Ford Part Number is the _base part code_. This describes the functionality of the part itself and, generally, where on the vehicle it goes. This code is often re-used across years and vehicles, and it is the only information that you can see on fordparts.com when looking at parts. This is the part number that parts departments normally consider when looking up part numbers for a specific make / model / year/ part code combination.

This is the copy/pasted table I can find online but it it only accounts for 5-digit part codes. Many modern part codes are 6 digits long.

* 1000 -1250 WHEELS/HUBS/DRUMS
* 2001 -2900 BRAKES
* 3000 -3764 FRONT SUSPENSION / STEERING
* 4000 -4296 REAR AXLE
* 4600 -4859 DRIVESHAFT
* 5000 -5176 FRAME
* 5200 -5299 EXHAUST
* 5300 -5499 FRONT SUSPENSION /STABILIZER
* 5550 -5832 REAR SPRINGS
* 6000 -6898 ENGINE BASE ASSEMBLY
* 6905 -7997 TRANSMISSION AND DRIVETRAIN / CLUTCH RELATED
* 8000 -8499 RADIATOR /GRILLE
* 8500 -8689 WATER PUMP AND FAN
* 9000 -9296 FUEL TANK /SUPERCHARGER
* 9301 -9420 FUEL PUMPS
* 9421 -9499 MANIFOLDS /CLAMPS/INTAKE AND EXHAUST
* 9500 - 9599 CARBURETORS/SUPERCHARGERS
* 9600 - 9699 AIR CLEANER
* 9700 - 9999 ACCELERATOR/CHOKE &LINKAGE
* 10500 - 10576 BATTERY/VOLTAGE REGULATOR
* 11000 - 11382 STARTER
* 11450 - 11688 LIGHTING/IGNITION SWITCH
* 12000 - 12425 IGNITION COIL/SPARK PLUGS/DISTRIBUTOR/CONDENSER
* 13002 – 14689 LAMPS/HORNS/WIRING
* 15000 – 15858 MISCELLANEOUS ACCESSORIES
* 16000 – 16999 FENDERS/HOOD
* 17248 – 17383 SPEEDOMETER/TACH
* 17402 – 17666 WINDSHIELD WIPERS/WASHER
* 17700 – 17999 MIRRORS AND BUMPERS
* 18000 – 18125 SHOCK ABSORBERS
* 18148 – 18249 COMFORT AND CONVENIENCE ACCESSORIES
* 18250 – 18699 HEATER
* 18800 – 18900 RADIO/SPEAKERS
* 19500 – 19585 CUSTOM ACCESSORIES
* 19600 – 19898 AIR CONDITIONING

## Revision

The last part of a Ford part number is the revision. The revision code can mean several things and is usually part-dependent.

For example, an -AC suffix when -AA and -AB parts exist may just indicate it's a different revision.

However, the [Parking Aid Module](/systems/modules/PAM.md) for the C-Max comes in two families, the -AA family and the -BA family. The -AA family does not support automatic parking modes, it's the -BA family that does.

Be wary of _jumps_ in revision codes, they may indicate different functionality across part numbers.

Another good example are Sync 3 APIM units. They have a vast array of revision codes that indicate things like model years, onboard MMC storage, navigation license, and other details that can determine whether the unit will work for a Sync 3 retrofit.
