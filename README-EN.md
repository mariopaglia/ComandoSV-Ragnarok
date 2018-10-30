# Project History

The "SV" command for Ragnarok was created in 2016 or earlier by **Rhulio Victor**, **Carlos Lain** and **Alexandre Leigo** in its [Version 1.0](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/v1.0), in 2017 was reformulated by **Mário Augusto Paglia** in its [Version 2.0](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/v2.0) and in October/2018 returned as Open Source.

## Technical information

**Current Version:** [3.6](https://github.com/agenciah1code/ComandoSV-Ragnarok/tree/master)  
**Operating Systems:** Linux  
**Distributions:** Tested and created in CentOS 6.  

[![Release](https://img.shields.io/github/release/agenciah1code/ComandoSV-Ragnarok.svg?label=version)](https://github.com/agenciah1code/ComandoSV-Ragnarok/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/releases/latest)
![GitHub top language](https://img.shields.io/github/languages/top/agenciah1code/ComandoSV-Ragnarok.svg)
[![GitHub issues](https://img.shields.io/github/issues/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)
[![GitHub forks](https://img.shields.io/github/forks/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/network)
[![GitHub stars](https://img.shields.io/github/stars/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/stargazers)
[![GitHub contributors](https://img.shields.io/github/contributors/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/graphs/contributors)
[![GitHub license](https://img.shields.io/github/license/agenciah1code/ComandoSV-Ragnarok.svg)](https://github.com/agenciah1code/ComandoSV-Ragnarok/blob/master/LICENSE)

## Available Functions

Up to this version, the following functions are available:

* **sv ligar** - Turn on the emulator (brAthena / Cronus / Hercules / rAthena / eAmods)
* **sv desligar** - Turn off the emulator (brAthena / Cronus / Hercules / rAthena / eAmods)
* **sv compilar** - Compile the emulator (brAthena / Cronus / Hercules)
* **sv compilar-cmake** - Compile emulator with CMAKE (specific emulators)
* **sv compilar-rathena** - Command specially created to compile rAthena emulators (GCC-C ++ version 5.X)
* **sv status** - Checks if the emulator has its processes turned on or off
* **sv screen** - Rotate the emulator in the background with the Screen **(POSSIBLELY WILL BE DISCONTINUED)**
* **sv retornar** - Returns to the screen of the Screen in the other accesses to the SSH **(POSSIBLELY WILL BE DISCONTINUED)**
* **sv preparar** - Gives the initial permissions to the emulator (chmod 777 configure and ./configure)
* **sv backup** - Creates a backup and a .zip file from the / home / emulator folder in / home / backup
* **sv baixar-emulador** - Download emulators directly from the official GitHub repositories (brAthena / Cronus / Hercules / rAthena)
* * **sv baixar-brathena** - Download the brAthena emulator at [official repository](https://github.com/brAthena/brAthena)
* * **sv baixar-brathena-old** - Download the brAthena emulator (Version 24/09/2018) in the [official repository](https://github.com/brAthena/brAthena20180924)
* * **sv baixar-cronus** - Download the Cronus emulator in the [official repository](https://github.com/Cronus-Emulator/Cronus)
* * **sv baixar-hercules** - Download the Hercules emulator in the [official repository](https://github.com/HerculesWS/Hercules/)
* * **sv baixar-rathena** - Download the rAthena emulator at [official repository](https://github.com/rathena/rathena)
* **sv compile-eamod** - Command specially created to compile eAmod emulators

## What will be implemented in the future?

In addition to constant corrections in the current functions, we also want the "SV" command to completely edit the emulator through the command line (terminal), we want to unify the parallel project [RagEditor - Linux](https://github.com/agenciah1code/rageditor-linux) to this project, making it a function called**"sv edit"**, in which additional parameters such as:

* **sv edit --ip** - Configure the IP of the map-server, char-server and login-server
* **sv edit --name** - Set server name in the emulator
* **sv edit --rates** - Set emulator rates
* **sv edit --level** - Set maximum emulator level
* **sv edit --drops** - Configure emulator drops
* **sv edit --re** - Configure the Emulator for Renewal
* **sv edit --pre-re** - Configure the Emulator for Pre-Renewal
* Do you have suggestions? [Leave it here!](Https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)

#### Project translation and commands for English

We would love your collaboration to translate the project, see how to contribute to the project in the sessions below

# How to install?

1. [Download the SV command](https://github.com/agenciah1code/ComandoSV-Ragnarok/archive/master.zip)
2. Extract the `sv` file into the` bin` folder of your Linux system
3. Run the `chmod +x /bin/sv` command
4. Test the `sv` digital function in your terminal

# Thanks

People who contributed to this project become possible:

* Rhúlio Victor
* Carlos Lain
* Alexandre Leigo
* Mário Augusto Paglia

## How to contribute to the project?

### Are you a programmer?

1. Realize a Project Fork
2. Make tests, changes, implementations or corrections
3. Submit a Pull Request

### Not a programmer?

If you are not a programmer, you have no problems, you can also contribute to the project through [this link.](Https://github.com/agenciah1code/ComandoSV-Ragnarok/issues)