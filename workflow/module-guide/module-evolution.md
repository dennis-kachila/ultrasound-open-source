# Ultrasound Module Evolution and Status Guide

This document provides comprehensive information about the evolution of modules in the ultrasound open-source project, helping you identify which modules are current, which are obsolete, and how to choose the right components for your functional ultrasound system.

## Module Status Overview

### Current Active Modules

These modules are the latest versions recommended for building a functional ultrasound system:

| Module | Purpose | Status | Introduced | Key Components |
|--------|---------|--------|------------|----------------|
| **matty** (un0rick) | All-in-one board | Latest flagship board | 2018 | ICE40 HX4K FPGA, integrated ADC, memory |
| **lit3rick** | All-in-one board | Newer alternative to matty | Post-2018 | ICE40 UP5K FPGA, improved specs |
| **pic0** | Pulse-echo device | Latest compact option | 2018 | RP2040 microcontroller |
| **lite.tbo** | High voltage pulser | Current pulser module | Post-2016 | HV pulser for transducer excitation |
| **goblin** | Analog processing | Current with v2 revision | 2016 (updated) | TGC, envelope detection |
| **doj** | Motherboard | Current for modular approach | 2016 | Interconnects between modules |
| **elmo** | ADC module | Current | 2017 | 20Msps, 9+ bit conversion |
| **silent** | Signal simulator | Current testing tool | 2016 | For testing without transducer |
| **retroATL3** | Transducer module | Still necessary hardware | 2016 | Mechanical transducer movement |
| **wirephantom** | Testing phantom | Current testing tool | 2016 | Wire-based calibration phantom |

### Retired/Obsolete Modules

These modules have been superseded by newer designs or are no longer maintained:

| Module | Original Purpose | Replacement | Why Obsolete |
|--------|-----------------|-------------|--------------|
| **tobo** | Original pulser | lite.tbo | Used older HV7360 (LFGA package) |
| **alt.tbo** | Alternative pulser | lite.tbo | Experimental design with issues |
| **oneeye** | Arduino controller | Integrated in newer designs | Limited capabilities |
| **mogaba** | Power supply | Integrated in newer designs | Standalone module no longer needed |
| **croaker** | STM32 controller | Integrated in newer designs | M3/M4 microcontroller approach abandoned |
| **toadkiller** | BeagleBone acquisition | Integrated in newer designs | BeagleBone approach replaced |
| **cletus** | Mechanical module | Integrated in retroATL3 | Interfaced transducer and servo |
| **tomtom** | Motor control | Integrated in newer designs | Standalone motor control not needed |
| **sleepy** | Case module | Custom cases for newer boards | Original case design obsolete |
| **loftus** | Unknown | Integrated in newer designs | Early prototype |
| **hannin** | WiFi module | Integrated in newer designs | EMW3165-based WiFi approach abandoned |

## Module Evolution Timeline

The project evolved through several distinct generations:

### Pre-2016: Initial Development
- **Murgen** - The original development kit, precursor to the modular approach

### 2016: First Modular Approach
- **tobo** - Original pulser module
- **goblin** - Analog processing module
- **oneeye** - Arduino-based control
- **mogaba** - Power supply module
- **cletus** - Mechanical module

### 2016-2017: Feature Expansion
- **doj** - Motherboard connecting modules
- **silent** - Signal simulation module
- **retroATL3** - Transducer module with mechanical movement
- **elmo** - ADC module

### 2017-2018: Integration and Refinement
- **lite.tbo** - Improved pulser replacing tobo
- **alt.tbo** - Alternative pulser design (later retired)

### 2018-Present: Consolidated Designs
- **matty** (un0rick) - All-in-one board with FPGA
- **lit3rick** - Newer all-in-one board with UP5K FPGA
- **pic0** - Compact RP2040-based solution

## Choosing the Right Modules

### Option 1: All-in-One Approach (Simplest)
- **Hardware**: matty (un0rick) + retroATL3
- **Advantages**: Simplest setup, minimal connections, well-documented
- **Best for**: Beginners, those wanting a quick start

### Option 2: Modern All-in-One Approach (Advanced)
- **Hardware**: lit3rick + retroATL3
- **Advantages**: Latest design, enhanced capabilities
- **Best for**: Advanced users, research applications

### Option 3: RP2040-Based Approach (Compact)
- **Hardware**: pic0 + retroATL3
- **Advantages**: Compact, good for educational purposes
- **Best for**: Educational environments, basic applications

### Option 4: Modular Approach (Most Flexible)
- **Hardware**: lite.tbo + goblin + doj + retroATL3 + elmo
- **Advantages**: Maximum flexibility, accessible test points
- **Best for**: Development, experimentation, learning the signal chain

## Official Status Changes

The project maintainer officially reorganized the modules on April 8, 2018, with the following changes:

> "@done Clean Modules list (keep lite.tbo, goblin, cletus, doj, elmo, matty) + add 'CNprobe'"
> 
> "@done Put alt.tbo, tobo, loftus, tomtom, croaker, retroATL3 and wirephantom in retired modules + add 'PU3090' phantoms in retired"

Note that despite being moved to "retired", modules like retroATL3 remain necessary for functional ultrasound systems and continue to be used in experiments.

## Component Availability Considerations

When building your system, consider these component availability factors:

1. **FPGA Availability**: The ICE40 HX4K (matty) and UP5K (lit3rick) are still manufactured but may have supply constraints

2. **RP2040 Availability**: The RP2040 microcontroller (pic0) has experienced shortages but is generally available

3. **HV Pulser ICs**: The newer HV7360 in CABGA package (used in lite.tbo) is preferred over the obsolete LFGA package (used in original tobo)

4. **Transducers**: The retroATL3 is based on salvaged equipment, so availability depends on finding donor equipment

## Recommended Development Path

For those new to ultrasound development, we recommend this progression:

1. **Start**: Begin with the pic0 + retroATL3 for basic understanding
2. **Intermediate**: Move to matty + retroATL3 for improved capabilities
3. **Advanced**: Either:
   - Adopt the modular approach with lite.tbo + goblin + doj for learning the complete signal chain, or
   - Use lit3rick + retroATL3 for the most advanced capabilities

## Documentation Priority

When consulting documentation, prioritize in this order:
1. Module-specific documentation in the respective folders
2. Workflow guides in the workflow directory
3. General documentation in the doc directory
4. Historical information in the Worklog.md file

This module evolution information has been compiled from analysis of the project repository as of May 2025.
