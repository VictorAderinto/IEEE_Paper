# Determining Relative Fault Severity for Real Time Transient Stability Analysis
## Overview of Metrics

To determine a metric with the highest correlation to fault severity, we examined a some power system quantities including:
*	Generator active and reactive power, rotor angle
*	Line active and reactive power,
*	Bus voltage, frequency, and angle
*	Interface active and reactive power
  
![Screenshot 2025-01-30 201315](https://github.com/user-attachments/assets/bb9b92d5-1e26-4f8b-9c85-dbd54305ab79)

From each of these quantities we derived 7 quantities:
* Sum of Max
* Sum of Min
* Sum of (Max - Min)
* Sum of (Last Value - First Value)
* Sum of Curve Area
* Sum of Curve Deviation
* Sum of Standard Deviation
