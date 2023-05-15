# Ford Module Configuration

[See the general overview first](./ford_module_overview.md).

Ford C-Maxes make use of both individual config and central config. They are structured in AsBuilt files from Ford differently, and FORScan exposes them via different systems.

## Individual Config

Individual configuration is set directly on each module independently.

Sometimes values need to be set the same in multiple locations for the vehicle to act correctly. Be careful when modifying values that have global applicability.

Some config values store the VIN of the vehicle, be cautious when sharing these configurations online if you do not wish to reveal your vehicle's VIN.

### Configuration Structure

Configuration flags are raw locations in the ECC memory of a module that are interpreted by the modules's firmware. The locations follow a common format.

| Module | Address   | Data           |
| ------ | --------- | -------------- |
| PSCM   | 730-01-01 | 0A6A 0196 5094 |

The address breaks down into three sections:

* The module address on the bus
* The config block number
* The line number within the block

A module always has a unique ID on the bus. It may have many blocks (such as the PCM) or very few (such as the GPSM), same with the number of lines per block. Documentation on the internet that has a different number of blocks and lines is a good indicator you're looking at something that doesn't apply to your vehicle.

The data is the set of bytes that are present at that data.

* Between 1 and 5 bytes of configuration
* Always a checksum byte at the end

Checksums are calculated from the full address (07300101) and data (0A6A019650) adding the bytes together (07 + 30 + 01 + 01 + 0A + 6A + 01 + 96 + 50) modulo 256 (94).

Meaning of configuration is _entirely_ left up to the module, that is, there is _no_ way to know what the meaning of a configuration value is without a guide _for your specific module's part number and firmware_ and _your vehicle's model year and installed components_. **Never assume configuration translates between different vehicles!**

### AsBulit File Format

### Finding AsBuilt Configurations

Anyone can download the AsBuilt Module Configuration map for a vehicle's VIN from [the Motorcraft website](https://www.motorcraftservice.com/AsBuilt).

You _should_ do this with your own vehicle as soon as possible _before_ you begin modifying things, so you have a backup to fall back to and perform diff calculations with.

You _can_ get VINs from the internet, especially used car websites, which can help inform how the configuration for various modules has changed over time. If you're adding a new feature or module to your vehicle you will need to know the configuration for what you want. Comparing the AsBuilt data for different VINs is how most people have reverse-engineered what the configuration flags do.

CyanLabs [has a fantastic database](https://cyanlabs.net/asbuilt-db/) of AsBuilt configurations and what they do. They deserve your money, donate to them if you use them.

### Modifying Configuration

> ⚠️ Some configuration bytes are write-once, and changes can't be undone. Do not change values blindly unless you have a guide to follow or backup plan (extra module, extra car, extra money) to recover.

FORScan Desktop can be used to view and modify module configuration, so long as you've purchased an extended license.

FORScan has two interfaces for configuring modules: GUI and Raw AsBuilt.

GUI mode is available for some configuration values on some modules, and lets you set the values of your modules using a click-through set of menus. This is reasonably safe to play around with as the valid values have been figured out for you.

Raw AsBuilt mode gives you an interface to modify the raw bytes in a config. This, of course, carries with it some risk that you enter a bad value and your vehicle misbehaves. Be careful, take backups, and write down what you did and what effect it had. Future-you will thank past-you for taking the effort.

FORScan will automatically recalculate a checksum for you when modifying values in raw mode.

### Special notes

The [PCM](./PCM.md) has a special block called the `Vehicle ID` or VID block. In older models this could only be set by modifying the module firmware using a special programming mode that involved hardware support (FEPS signal). This doesn't appear to apply to C-Maxes which are newer than FEPS PCMs.

The TCM in other vehicles also has special rules, but C-Maxes have an [SOBDMC](./SOBDMC.md) instead of a TCM so it doesn't apply.

## Central Configuration

Central Configuration is a special block of memory in the [Body Control Module](./BdyCM.md) that stores a lot of common configuration settings for the entire vehicle. This is commonly where configuration that affects multiple modules at the same time will be stored. But also it can be where somewhat random stuff gets tossed.

Central Configuration is often abbreviated CC.

### AsBuilt File Format for CC

TODO!

### Modifying CC

The above notes about the Motorcraft website and FORScan apply to CC, however FORScan does not expose the raw CC values for modification. Instead there is only a GUI editor option.

The GUI editor for FORScan is fairly comprehensive and covers nearly all of the CC fields that anyone might want to set, and all of the values C-Max owners might want to modify. I cover these values in the [BdyCM docs](./BdyCM.md).

## Sources

* [FORScan thread on module configuration](https://forscan.org/forum/viewtopic.php?t=17208)
* [FORScan thread on central configuration](https://forscan.org/forum/viewtopic.php?f=16&t=1932)
