# Ultrasound Data Processing Guide

This guide explains how to process the raw ultrasound data from your device to generate meaningful ultrasound images.

## Software Requirements

1. **Development Environment**
   - Python 3.6+ with NumPy, SciPy, Matplotlib
   - Jupyter Notebook (recommended for visualization)
   - Optional: MATLAB for advanced processing

2. **Device-Specific Drivers**
   - For matty/un0rick: FPGA communication libraries
   - For lit3rick: Device-specific drivers
   - For pic0: Serial communication libraries

3. **Image Processing Libraries**
   - OpenCV for image processing
   - scikit-image for advanced imaging techniques

## Data Acquisition

1. **Establishing Connection**
   - Connect your device via USB
   - Install required drivers if not automatically recognized
   - Verify connection using device manager or system tools

2. **Configuring Acquisition Parameters**
   - Set sampling frequency
   - Configure acquisition depth
   - Set number of lines per frame
   - Adjust pulse repetition frequency

3. **Capturing Raw Data**
   - Use provided acquisition scripts:
     - For matty/un0rick: `python acquire_matty.py`
     - For lit3rick: `python acquire_lit3rick.py`
     - For pic0: `python acquire_pic0.py`
   - Save raw data in appropriate format (usually CSV or binary)

## Basic Signal Processing

1. **Data Loading**
   ```python
   import numpy as np
   data = np.loadtxt('raw_data.csv')
   # Or for binary data
   data = np.fromfile('raw_data.bin', dtype=np.int16)
   ```

2. **DC Offset Removal**
   ```python
   data_no_dc = data - np.mean(data, axis=0)
   ```

3. **Filtering**
   ```python
   from scipy import signal
   # Bandpass filter around transducer frequency
   b, a = signal.butter(3, [fL/(fs/2), fH/(fs/2)], 'bandpass')
   filtered_data = signal.filtfilt(b, a, data_no_dc)
   ```

4. **Envelope Detection**
   ```python
   # Using Hilbert transform
   from scipy.signal import hilbert
   analytic_signal = hilbert(filtered_data)
   envelope = np.abs(analytic_signal)
   ```

5. **Log Compression**
   ```python
   # Dynamic range compression for better visualization
   log_compressed = 20 * np.log10(envelope + 1e-10)
   ```

## Image Formation

1. **Scan Conversion**
   - For linear arrays: Direct mapping of scan lines
   - For sector scans (retroATL3): Polar to Cartesian conversion
   ```python
   # Example for sector scan conversion
   import numpy as np
   
   def sector_scan_conversion(data, num_lines, start_angle, end_angle, max_depth, image_size):
       angle_step = (end_angle - start_angle) / (num_lines - 1)
       angles = np.linspace(start_angle, end_angle, num_lines)
       
       # Create empty image
       image = np.zeros(image_size)
       
       # Fill image pixel by pixel
       for y in range(image_size[0]):
           for x in range(image_size[1]):
               # Convert cartesian coordinates to polar
               # Origin at top center of image
               cart_x = x - image_size[1]/2
               cart_y = y
               
               r = np.sqrt(cart_x**2 + cart_y**2)
               theta = np.arctan2(cart_x, cart_y)
               
               # Check if within scan sector
               if start_angle <= theta <= end_angle and r <= max_depth:
                   # Find nearest scan line and sample
                   line_idx = int((theta - start_angle) / angle_step + 0.5)
                   sample_idx = int(r / max_depth * data.shape[1] + 0.5)
                   
                   if 0 <= line_idx < num_lines and 0 <= sample_idx < data.shape[1]:
                       image[y, x] = data[line_idx, sample_idx]
       
       return image
   ```

2. **B-Mode Image Creation**
   ```python
   import matplotlib.pyplot as plt
   
   # Create B-mode image from processed data
   plt.figure(figsize=(10, 8))
   plt.imshow(processed_data, cmap='gray', aspect='auto')
   plt.title('B-Mode Ultrasound Image')
   plt.colorbar(label='Intensity (dB)')
   plt.xlabel('Lateral Distance')
   plt.ylabel('Depth')
   plt.savefig('bmode_image.png', dpi=300)
   plt.show()
   ```

3. **Additional Processing Options**
   - Speckle reduction filters
   - Contrast enhancement
   - Edge detection for feature highlighting

## Advanced Processing Techniques

1. **Doppler Processing**
   - If your system captures multiple frames
   - Useful for blood flow visualization

2. **3D Reconstruction**
   - From multiple 2D slices
   - Requires position tracking or controlled sweep

3. **Tissue Characterization**
   - Spectral analysis of RF data
   - Texture analysis of B-mode images

## Calibration

1. **Spatial Calibration**
   - Use phantom with known dimensions
   - Calculate pixels-to-distance ratio

2. **Intensity Calibration**
   - Use standard reflectors with known reflectivity
   - Normalize echo intensities

## Data Export

1. **Image Export**
   - Save as standard formats (PNG, JPEG)
   - Consider DICOM format for medical applications

2. **Raw Data Archiving**
   - Save preprocessed data for future analysis
   - Document acquisition parameters

## Example Processing Pipeline

```python
# Complete example pipeline
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal
from scipy.signal import hilbert

# 1. Load data
raw_data = np.loadtxt('raw_data.csv')

# 2. Remove DC offset
data_no_dc = raw_data - np.mean(raw_data, axis=0)

# 3. Apply bandpass filter
fs = 40e6  # Sample frequency (40 MHz)
fL = 2e6   # Lower cutoff (~2 MHz)
fH = 5e6   # Upper cutoff (~5 MHz)
b, a = signal.butter(3, [fL/(fs/2), fH/(fs/2)], 'bandpass')
filtered_data = signal.filtfilt(b, a, data_no_dc)

# 4. Envelope detection
analytic_signal = hilbert(filtered_data)
envelope = np.abs(analytic_signal)

# 5. Log compression
log_compressed = 20 * np.log10(envelope + 1e-10)

# 6. Scan conversion (simplified example for linear array)
processed_image = log_compressed

# 7. Display image
plt.figure(figsize=(10, 8))
plt.imshow(processed_image, cmap='gray', aspect='auto')
plt.title('Processed Ultrasound Image')
plt.colorbar(label='Intensity (dB)')
plt.xlabel('Lateral Distance')
plt.ylabel('Depth')
plt.savefig('ultrasound_image.png', dpi=300)
plt.show()
```

## Next Steps

After successfully processing your ultrasound data:
1. Experiment with different processing parameters
2. Consider implementing real-time processing if needed
3. Explore advanced imaging techniques specific to your application
