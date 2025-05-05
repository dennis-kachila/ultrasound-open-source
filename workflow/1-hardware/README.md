# Hardware Selection Guide

This guide helps you select the appropriate modules for your ultrasound device based on your requirements and expertise level.

## Essential Modules Overview

### Signal Generation
- **lite.tbo**: High voltage pulse generator that creates the electrical pulses needed for ultrasound imaging
  - Voltage: Up to 100V
  - Pulse width: Configurable
  - Key components: HV7360 pulser IC

### Transducer Interface
- **retroATL3**: Salvaged transducer with mechanical movement
  - Frequency: ~3.5MHz
  - Type: Tri-piezo head
  - Mechanical sweeping for B-mode imaging

### Signal Acquisition & Processing
- **goblin**: Analog processing module for Time Gain Compensation and envelope detection
  - ADC resolution: 8-bit
  - Variable gain: 0-40dB
  - Envelope detection built-in

### System Integration & Control
Choose one of:
- **matty/un0rick**: All-inclusive board with ICE40 HX4K FPGA
  - Complete solution with ADC, memory and control
  - USB interface for data transfer
  - Good SNR and data acquisition capabilities

- **lit3rick**: Newer all-in-one board with ICE40 FPGA
  - Integrates pulse generation and signal acquisition
  - More modern design with improved specifications

- **pic0**: RP2040-based pulse-echo device
  - Simpler approach using microcontroller
  - Good for educational purposes and basic imaging
  - Lower cost solution

### Connectivity
- **doj**: Motherboard connecting different modules together
  - Required for modular approach
  - Provides easy access to signals between modules

### Testing
- **silent**: Module that simulates raw signals
  - Useful for testing without an actual transducer
  - Provides reference signals for development

## Configuration Selection Guide

### Beginner Level Configuration
For those new to ultrasound imaging:
- **pic0** + **retroATL3**
- Simplest configuration with minimal components
- Limited imaging capabilities but good learning platform

### Standard Configuration
For general-purpose imaging:
- **retroATL3** + **lite.tbo** + **goblin** + **matty/un0rick** + **doj**
- Complete modular system
- Good balance of flexibility and performance

### Advanced Configuration
For research and development:
- **retroATL3** + **lit3rick**
- Highest performance solution
- Greatest flexibility for experimentation

## Bill of Materials

Depending on your selected configuration, gather:
1. Selected core modules
2. Connecting cables and adaptors
3. Power supply appropriate for your modules
4. Computer for data acquisition and processing
5. Basic electronic tools (soldering iron, multimeter, etc.)

## Next Steps

Once you've selected your configuration and gathered the components:
1. Proceed to [Assembly Guide](../2-assembly/README.md)
2. Review module-specific documentation for detailed specifications
