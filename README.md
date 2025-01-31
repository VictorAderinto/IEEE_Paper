# Determining Relative Fault Severity for Real Time Transient Stability Analysis
## Overview of Metrics

To determine a metric with the highest correlation to fault severity, we examined power system quantities including:
*	Generator active and reactive power, rotor angle
*	Line active and reactive power,
*	Bus voltage, frequency, and angle
*	Interface active and reactive power

During transient simulation, data from multiple buses, generators, or lines are recorded for each quantity above. A sample is shown below:
<img src="https://github.com/VictorAderinto/IEEE_Paper/blob/main/Quantity%20Measurement.png" alt="Bus Voltage Simulation Data" width="500"/>

For each quantity we then derive 7 metrics using the recorded simulation data:
* Sum of Max
* 
 <img src="https://github.com/VictorAderinto/IEEE_Paper/blob/main/Sample%20Graph.png" width="400"/>

* Sum of Min
* Sum of (Max - Min)
* Sum of (Last Value - First Value)
* Sum of Curve Area
* Sum of Curve Deviation
* Sum of Standard Deviation
