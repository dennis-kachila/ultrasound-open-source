# All-in-One Ultrasound Build Approach

This guide provides detailed instructions for building a functional ultrasound system using one of the all-in-one board options.

## Options Overview

You can choose from three primary all-in-one approaches:

1. **matty (un0rick)** - The original all-inclusive board with ICE40 HX4K FPGA
2. **lit3rick** - The newer generation all-in-one board with enhanced capabilities
3. **pic0** - The compact RP2040-based pulse-echo device

## Option 1: matty (un0rick) Build

### Components Required
- [matty](../matty) (un0rick) board
- [retroATL3](../retroATL3) transducer or compatible ultrasound probe
- 5V power supply
- USB cable (for data transfer)
- Computer with appropriate software

### Assembly Steps

1. **Preparation**
   - Inspect the matty board for any physical damage
   - Identify all connectors: power, transducer, USB/data

2. **Power Setup**
   - Connect the 5V power supply to the power input on the matty board
   - Double-check polarity before powering on

3. **Transducer Connection**
   - Identify the transducer connector on matty (labeled on board)
   - Carefully connect the retroATL3 transducer
   - Ensure firm connection to avoid signal loss

4. **Computer Interface**
   - Connect the USB cable from matty to your computer
   - Install any required drivers from the matty documentation

5. **Software Configuration**
   - Load the appropriate software from the matty documentation
   - Configure parameters according to your transducer specifications
   - Set up acquisition parameters (depth, gain, etc.)

### Testing Verification

1. **Initial Power Test**
   - Apply power and verify power LEDs illuminate
   - Check for any error indicator lights

2. **Connection Test**
   - Verify computer recognizes the matty board
   - Test communication interface

3. **Basic Imaging Test**
   - Apply ultrasound gel to a simple test target
   - Perform a basic scan to verify image formation
   - Check for expected echo patterns

## Option 2: lit3rick Build

### Components Required
- [lit3rick](../lit3rick) board
- [retroATL3](../retroATL3) transducer or compatible ultrasound probe
- Power supply (according to lit3rick specifications)
- Data interface cables
- Computer with compatible software

### Assembly Steps

1. **Preparation**
   - Inspect the lit3rick board carefully
   - Identify all connection points and interfaces

2. **Board Configuration**
   - Configure any jumpers or switches according to documentation
   - Prepare the FPGA configuration if required

3. **Connections**
   - Connect power supply to the lit3rick board
   - Connect transducer to the appropriate connector
   - Set up data interface to computer

4. **Software Setup**
   - Load the lit3rick firmware as needed
   - Configure the acquisition software
   - Set parameters appropriate for your application

### Testing Verification
- Follow similar verification steps as with the matty board
- Refer to specific lit3rick documentation for test points and expected signals

## Option 3: pic0 Build

### Components Required
- [pic0](../pic0) RP2040-based device
- [retroATL3](../retroATL3) transducer or compatible probe
- Power supply compatible with pic0
- USB cable for computer interface
- Computer with appropriate software

### Assembly Steps

1. **Preparation**
   - Inspect the pic0 board
   - Identify all connections and interfaces

2. **Connections**
   - Connect power to the pic0 board
   - Connect the transducer to the appropriate connector
   - Connect USB interface to computer

3. **Software Setup**
   - Load the pic0 firmware
   - Set up acquisition software
   - Configure parameters for your application

### Testing Verification
- Power on and verify startup sequence
- Test communication with computer
- Perform basic echo detection test
- Verify signal quality and imaging capability

## Advantages and Limitations

| Approach | Advantages | Limitations |
|----------|------------|-------------|
| matty (un0rick) | Well-documented, complete solution | Less flexible for customization |
| lit3rick | Latest design, enhanced capabilities | More complex to set up initially |
| pic0 | Compact, accessible microcontroller | Limited processing power compared to FPGA solutions |

## Next Steps

After successful assembly and basic verification:
1. Proceed to the [testing guide](testing-guide.md) for more detailed verification
2. Explore software options for image processing and analysis
3. Calibrate your system for optimal performance
