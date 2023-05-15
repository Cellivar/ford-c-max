# Ford Elecrical Architecture Notes

> ⚠️ These notes are my understanding that I use to apply modifications to my car. They are almost certainly inaccurate, missing details, and using non-Ford terminology. If you can correct or improve these, _especially_ if you can cite more authoritative resources [I'm _very_ open to hearing about it!](https://github.com/Cellivar/ford-c-max/issues/new/choose)

As with any complex system, Ford has an overall design architecture for vehicle platforms that were re-used across multiple generations and models of vehicles. These architectures included things like common configuration, CAN bus message packets, and other details that allowed vehicle modules to work together.

The different electrical architectures define how related the modules and module firmware is for a given vehicle. This can help determine, for example, whether a module off a Ford Escape will work in a C-Max. This will also inform you how to alter the configuration of vehicle modules when altering their settings.

## The US Hybrid C-Max Platform

The 2013-2018 C-Max Hybrid sold in the US and Canadian markets is a [second-gen C1 vehicle platform](https://en.m.wikipedia.org/wiki/Volvo_P1/Mazda_BK/Ford_Global_C-car_Platform) or "Global C-Car", designation `C344`. This was the second revision of the C-Max vehicle, the original exclusive to Europe markets.

_Generally speaking_ a C-Max is mostly C1MCA architecture, with a steadily increasing amount of CGEA 1.2 equipment towards the end of the model.

The C-Max occupies an unfortunate location in the development history of Ford vehicles as it's straddling the transition period from C1MCA to CGEA 1.2/1.3 architectures. This means the answer to "what platform does my C-Max use" depends on the year, programming of various modules, and of course _what mods you have done to it_. For example, a [Sync 3 APIM](./modules/APIM.md) will end up communicating both C1MCA and CGEA messages on the CAN bus because it expects a mixture of both.

C1MCA architecture features include:

* [Central Configuration](./modules/ford_module_config.md) for some vehicle behavior.
* [Individual module configuration](./modules/ford_module_config.md) for additional behavior.
* [FMFU module updating](./modules/ford_module_updating.md).
* 3 CAN busses, (HS-CAN, MS-CAN, I-CAN).
* Gateway Module acting as bus master.

The Fusion and C-Max were developed closely as both share significant portions of parts, however a Fusion was first designed as a CGEA vehicle. This means it lacks the transition confusion and, generally, results in an easier-to-modify vehicle. **This means information you find on the internet for the Fusion may or may not map to the C-Max**. Just because they share the same drivetrain doesn't mean they're programmed the same way!

## Electrical Architectures

### C1MCA (Global C-Car platform)

Known vehicles:

* C-Max 2013-2018
* Focus 2011-2018 (MK 3, 3.5, including Electric)
* Fiesta 2008-2019 (MK 6, 6.5)
* Escape/Kuga 2013-2019
* Transit Connect 2012-2019? (Unclear if post-2019 facelift is CGEA)

The C1MCA architecture is no longer used after Ford transitioned to CGEA 1.3 and the FNV architecture, alongside the shut down of nearly all light vehicle production in 2019.

### CGEA

Ford's Common Global Electrical Architecture

Known vehicles:

* CGEA 1.2
  * Fusion 2013-2015(?)
  * F150 2009-2014
  * Edge 2009-2014
  * Explorer 2011-2014
  * F250+ 2009-2016
  * Flex 2009-2019
  * Taurus 2010-2019
* CGEA 1.3
  * Fusion 2016-2020(?)
  * F150 2015-2020
  * Edge 2015-2022?
  * Explorer 2015-2022?
  * F250+ 2017-2022?

CGEA 1.3 added a dedicated Gateway Module (GWM) as a network hub, which caused some bus clock masters to change. This can cause some modules (such as IPCs) to be incompatible across CGEA 1.2 and 1.3 vehicles.

Current CGEA vehicles are transitioning to FNV, with FNV seeming to be mostly an iteration of CGEA 1.3.

### FNV and FNV-2

Known vehicles for FNV2:

* Mustang Mach-E 2021+
* F150 2021+
* F250+ 2023+
* Bronco 2021+
* Escape 2023+

Introduced the Mustang Mach-E 2021 model the Ford Networked Vehicle platform is the evolution of CGEA to introduce wideband Ethernet to the vehicle network bus. This is designed to allow OTA updates of module firmware along with supporting the ever increasing amount of traffic on vehicle data busses originally intended to do little more than smog checks.

OTA updates for modules are VIN-locked, so migrating modules between vehicles will be harder. Sync 4 APIMs are designed for the FNV platform and do not have any C1MCA compatibility. FNV uses a new set of network busses and a gateway module that is a significant departure from previous platforms. Compatibility hacks to retrofit any of this into a C1MCA platform vehicle is beyond my interest.

## See also

* [Ford module details](./modules/ford_module_overview.md).

## Sources

* [MIT paper on CGEA](https://dspace.mit.edu/handle/1721.1/59222)
* [Wikipedia article on Ford platforms](https://en.wikipedia.org/wiki/List_of_Ford_platforms)
