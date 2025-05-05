# Ultrasound System Assembly Guide

This guide provides step-by-step instructions for assembling your open-source ultrasound system based on your chosen configuration.

## Pre-Assembly Checklist

- Ensure all modules are in working condition
- Gather necessary tools: screwdrivers, pliers, soldering iron, wire cutters
- Prepare appropriate workspace with antistatic precautions
- Review individual module datasheets and connection diagrams

## Assembly Instructions by Configuration

### Modular Configuration (doj + separate modules)

1. **Prepare the doj motherboard**
   - Inspect the connectors and traces
   - Position the motherboard on your workspace

2. **Connect the lite.tbo pulser module**
   - Attach to the corresponding connectors on the doj board (J1 and J3)
   - Secure with mounting hardware if applicable

3. **Connect the goblin analog processing module**
   - Connect to the signal path connectors on the doj motherboard (J4 and J5)
   - Verify correct orientation of connectors

4. **Connect the matty/un0rick controller board**
   - Attach to the digital I/O connectors on doj (J7)
   - Connect USB cable for data transfer and power

5. **Connect the retroATL3 transducer**
   - Connect to the transducer input on the lite.tbo pulser
   - Secure cable connections with appropriate strain relief

6. **Power connections**
   - Connect power supply to the appropriate inputs
   - Double-check voltage levels before powering on

7. **Connect to computer**
   - Use USB cable from matty/un0rick to your computer
   - Install necessary drivers (see software guide)

### All-in-One Configuration (lit3rick or matty/un0rick)

1. **Prepare the all-in-one board**
   - Inspect the board and connectors
   - Place in appropriate enclosure if available

2. **Connect the retroATL3 transducer**
   - Connect directly to the transducer input on the board
   - Secure cable connections

3. **Power connections**
   - Connect appropriate power supply
   - Verify voltage requirements (typically 5V via USB)

4. **Connect to computer**
   - Connect USB cable to your computer
   - Install necessary drivers

### Simplified Configuration (pic0)

1. **Prepare the pic0 board**
   - Inspect the RP2040-based board
   - Position in your workspace

2. **Connect the retroATL3 transducer**
   - Connect to the transducer input on pic0
   - Secure connection

3. **Power and data connection**
   - Connect USB cable for both power and data transfer
   - The RP2040 should appear as a USB device

## Interface Verification

1. **Visual inspection**
   - Verify all connections are secure
   - Check for any loose wires or poor connections

2. **Continuity testing**
   - Use multimeter to verify electrical continuity between modules
   - Check for any shorts or open circuits

3. **Power-on test**
   - Apply power and check for status LEDs
   - Monitor for any unusual heating or smells

## Mechanical Assembly

1. **Transducer positioning**
   - Mount the retroATL3 transducer on a stable fixture
   - Allow for appropriate movement if using mechanical scanning

2. **System stability**
   - Secure all modules to prevent movement during operation
   - Minimize cable strain

## Next Steps

Once your system is assembled:
1. Proceed to the [Testing Guide](../3-testing/README.md)
2. If you encounter issues, refer to the troubleshooting section of each module's documentation
