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

<img src="https://github.com/VictorAderinto/IEEE_Paper/blob/main/Sample%20Graph.png" width="400"/>

* **Sum of Max**: Sum of the maximum value across all measurements for a quantity. From the sample graph above, **0.44** is the maximum value, this is added to the maximum values across all other measurements for that quantity.
* **Sum of Min**: Sum of the minimum value across all measurements for a quantity. From the sample graph above, **0.25** is the minimum value, this is added to the minimum values across all other measurements for that quantity.
* **Sum of (Max - Min)**: Sum of the max-min value across all measurements for a quantity. From the sample graph above, 0.44 - 0.25 = **0.19** is the max-min value, this is added to the max-min values across all other measurements for that quantity.
* **Sum of (Last Value - First Value)**: : Sum of the last-first value across all measurements for a quantity. From the sample graph above, 0.34 - 0.35 = **-0.01**  is the last-first value, this is added to the last-first values across all other measurements for that quantity.
* **Sum of Curve Area**: Sum of the absolute value of the area between the line and the curve. This value is calculated and summed across all measurements for that quantity. 
* **Sum of Curve Deviation**: 
* **Sum of Standard Deviation**: Sum of the standard deviation across all measurements for a quantity.

| Quantity | Metric | Aggregate Ranking Error |
|----------|----------|----------|
| Row 1 Col 1 | Sum of Max | Row 1 Col 3 |
| Row 2 Col 1 | Sum of Min | Row 2 Col 3 |
| Row 3 Col 1 | Sum of (Last - First) | Row 3 Col 3 |
| Row 1 Col 1 | Sum of (Max - Min) | Row 1 Col 3 |
| Row 2 Col 1 | Sum of Curve Area | Row 2 Col 3 |
| Row 3 Col 1 | Sum of Curve Deviation | Row 3 Col 3 |
| Row 3 Col 1 | Sum of Standard Deviation | Row 3 Col 3 |
