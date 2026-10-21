# Ford Electrical Module Overview

[You may want to start with the ford platform overview](/systems/ford_platform_overview.md).

Since the late 90s Ford vehicles have used a control module architecture that allowed individual modules to be serviced from the CAN bus instead of having dedicated module programming connections. This system, referred to as the `Ford Module Firmware Update` procedure, or FMFU, is what enables over-the-bus updating of module firmware.

Starting in the late 2000s Ford greatly expanded the number of modules built on the common electronic module structure and began packing the functionality into every cost-effective chunk of the vehicle they could. This also coincided with their strong push to make vehicle parts more interchangeable, and resulted in significant cross-compatibility for modules and different vehicles. This is part of what makes owning a C-Max exciting, there's lots of existing documentation and tooling on these modules!

This article will focus on [C1MCA and CGEA 1.2-1.3 era architectures](/systems/ford_platform_overview.md) as that's what matters for the C-Max.

## Hardware and Firmware Structure

```mermaid
stateDiagram-v2
    state Microcontroller {
        state ROM {
            state "Primary Boot Loader" as PBL
        }
        state Flash {
            state "Executable (Strategy) 1" as exe
            state "Data (Calibration) 1" as cal
            state "Data M (Configuration) N" as data

            exe --> cal
            cal --> data
        }
        state EEPROM {
            state "Factory Config (AsBuilt)" as asbuilt
            state "Module data" as mdata
            asbuilt --> mdata
        }
        state RAM {
            state "Module data" as rmdata
        }
    }
    state "Secondary Boot Loader (SBL)" as SBL

    ROM --> Flash
    Flash --> EEPROM
    EEPROM --> RAM
    SBL --> RAM
```

This is a simplified diagram, actual memory structure layout can be all over the place. There can be multiple ROM segments between EEPROM segments, and ability to modfiy the ROM is only prevented by the FMFU process, it's not actually a separate memory segment.

The microcontroller (MCU) boots the Primary Boot Loader at the start of the memory block. This implements MCU startup, a fallback dealer recovery communication mode, and loads the application executable for actual module functionality.

Ford refers to the MCU application as a "Strategy" file, this is the application controlling the module in normal operation.

The application relies on configuration data, sometimes "Calibration" or "Configuration" in Ford's parlance.

Updating module firmware requires a module reboot, as normal application execution disables the FMFU bootloader functionality.

### Module Calibration Level

The combination of

* Physical part number
* Strategy part number
* Calibration part number

is calculated together into a _Calibration Level_, a dynamically generated value from the multiple inputs that determines what the correct combination of programmables on the module are.

FORScan handles most of this dynamically and employs Dark Magic to figure it all out. Further evidence the cost of their tool is worth it.

[See this document for more about module firmware updating](./ford_module_updating.md).

## Central and Distributed Configuration

A given module will have built-vehicle-specific configuration flags that must be set for the module to operate properly. These flags can come from multiple sources and are stored in different ways:

* Individual config: Flags stored directly on the module itself.
* Central config (CC): Flags stored in a central module (usually the [Body Control Module](./BdyCM.md)) and read by other modules over the network.

This configuration is generally referred to on the internet as `As-Built` or `AsBuilt`. In official documentation this actually refers to _a specific configuration_ that was programmed at the factory as part of vehicle manufacture.

C-Maxes distribute the system configuration between central and individual configuration on modules. This means some modules do not have any configuration options and won't show up in the editor in FORScan, instead those values are set in the Central Config.

[See this document for more about module config](./ford_module_config.md).

## CAN Bus Segmentation and the OBD Ports

C-Maxes (CGEA 1.2) split their modules across two CAN buses, both reachable from the OBD port:

* **HS-CAN**: 500 kbps, OBD pins 6 and 14
* **MS-CAN**: 125 kbps, OBD pins 3 and 11

Modules answer standard UDS requests on their AsBuilt module code as the request ID (e.g. `7D0`), and reply from request ID + 8 (e.g. `7D8`).

An empirical sweep (UDS `3E 00` TesterPresent, vehicle in RUN, modules awake) on a 2014 Energi produced this census:

| Bus   | Modules                                                                     |
| ----- | --------------------------------------------------------------------------- |
| HS-CAN | PCM (7E0), GWM (716), BdyCM (726), RCM (737), ABS (760), APIM (7D0), PSCM (730), OCS (765), SASM (797) |
| MS-CAN | GPSM (701), IPC (720), ACM (727), RFA (731), HVAC (733), DDM (740), PDM (741), TCU (754), FCIM (7A7), DACMC (7D5) |

Not located from the OBD port during this sweep: SOBDM (7E2), BECM (7E4), SOBDMC (7E6) — these addresses were not tried — and RGTM (775) and IPMB (7B1), which did not answer on MS-CAN and were not retried on HS-CAN. TODO: complete the census.

**Your adapter matters here.** Cheap ELM327 clones are hardwired to pins 6/14 and cannot reach MS-CAN at all (see [OBD adapters](/tools/obd_adapters.md)) — a sweep from a clone will only ever find the HS-CAN half of the car and may lead you to believe sleeping MS-CAN modules are missing.

### The Energi's Two OBD Ports

At least some C-Max Energis have _two_ J1962 diagnostic connectors:

1. Behind the hatch below the headlight controls (driver's side of the dash)
2. In the footwell below the steering wheel (the conventional location, behind which the [GWM](./GWM.md) lives)

Both were empirically confirmed to be wired in parallel — an identical set of modules answered from either port. The second port is a convenience, not a different bus.

## Sources

* [FORScan thread on module firmware architecture](https://forscan.org/forum/viewtopic.php?f=13&t=18751)
* [FORScan thread on module configuration](https://forscan.org/forum/viewtopic.php?t=17208)
* [FORScan thread on central configuration](https://forscan.org/forum/viewtopic.php?f=16&t=1932)
* [MIT paper on CGEA](https://dspace.mit.edu/handle/1721.1/59222)
