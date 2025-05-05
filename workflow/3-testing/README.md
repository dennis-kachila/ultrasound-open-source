# Ultrasound System Testing Guide

This guide helps you verify that your assembled ultrasound system is functioning correctly, from basic hardware tests to full imaging capabilities.

## Initial Power-Up Tests

1. **Visual Inspection**
   - Check that all status LEDs are functioning normally
   - Look for any components that are heating abnormally
   - Verify fans or cooling systems are operational (if applicable)

2. **Power Supply Verification**
   - Measure voltage at test points to confirm proper supply voltage
   - Check current draw is within expected parameters
   - Verify stable power under load conditions

3. **Communication Test**
   - Verify USB connection is recognized by the computer
   - Check that serial port or other interfaces are functioning
   - Test basic command and control capabilities

## Signal Path Verification

1. **Pulser Test (lite.tbo)**
   - Use an oscilloscope to verify pulse generation
   - Check pulse amplitude (~100V peak)
   - Verify pulse width and timing
   - Test pulse repetition frequency capabilities

2. **Analog Processing Test (goblin)**
   - Inject test signal at input
   - Verify signal amplification through gain stages
   - Test time gain compensation functionality
   - Verify envelope detection is working

3. **Acquisition System Test**
   - Check ADC functionality by capturing test signals
   - Verify data transfer to computer
   - Measure sample rate and buffer capacity

## Using the Silent Module for Test Signals

The silent module is a valuable tool for system testing as it provides simulated ultrasound signals:

1. **Connect the silent module** in place of the transducer
2. **Configure for test pattern** generation
3. **Capture and analyze** the simulated signals
4. **Compare with expected** reference patterns

## Transducer Testing

1. **Electrical Testing**
   - Measure transducer impedance (should be ~50 ohms ±20%)
   - Check for shorts or open circuits
   - Verify cable integrity

2. **Basic Echo Testing**
   - Use a simple test phantom (water tank with reflector)
   - Verify echo reception
   - Measure signal-to-noise ratio
   - Check for expected echo timing based on distance

3. **Mechanical Scanning Test (for retroATL3)**
   - Verify smooth mechanical movement
   - Test full range of motion
   - Check position feedback (if available)

## End-to-End Testing

1. **Phantom Testing**
   - Use a standard ultrasound phantom if available
   - If no commercial phantom is available, create a simple one with objects in water
   - Verify system can detect objects at known positions
   - Measure lateral and axial resolution

2. **Image Formation Test**
   - Capture full frame data
   - Process data to form B-mode image
   - Verify image corresponds to physical phantom

3. **Performance Benchmarks**
   - Measure frame rate capabilities
   - Check system stability during extended operation
   - Quantify image quality metrics (contrast, resolution, penetration depth)

## Troubleshooting Common Issues

1. **No pulse output**
   - Check power connections to lite.tbo
   - Verify trigger signals are present
   - Check for blown fuses or damaged MOSFETs

2. **No received signal**
   - Verify transducer connection
   - Check gain settings in goblin module
   - Test with silent module to isolate the issue

3. **Poor image quality**
   - Adjust TGC settings
   - Check for electrical noise sources
   - Verify proper grounding of all components
   - Optimize acquisition parameters

4. **Communication errors**
   - Update USB drivers
   - Check cable connections
   - Verify baud rate and communication settings

## Next Steps

Once your system passes these tests:
1. Proceed to the [Processing Guide](../4-processing/README.md)
2. Document baseline performance for future reference
3. Consider system calibration for improved accuracy
