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
* **Sum of Curve Deviation**: For each measurement, the difference between consecutive values is squared, summed together, and averaged i.e. 1/N (Y1 - Y2) ^2+ (Y2 - Y3)^2 +⋯.., This value is determined for all the measurements for that quantity and then summed together.
* **Sum of Standard Deviation**: Sum of the standard deviation across all measurements for a quantity.

The above metrics were calculated for each power system quantity and an aggregrate ranking error was derived to demonstrate correlation with severity, where lower value implies higher correlation. The results are summarized in the table below:

| Quantity                | Metric                    | Aggregate Ranking Error |
|-------------------------|---------------------------|-------------------------|
| Generator Active Power  | Sum of Max                | 1.73                    |
|                         | Sum of Min                | 0.46                    |
|                         | Sum of (Last – First)     | 20.06                   |
|                         | Sum of (Max – Min)        | 0.32                    |
|                         | Sum of Curve Area         | 0.86                    |
|                         | Sum of Curve Deviation    | 0.57                    |
|                         | Sum of Standard Deviation | 0.28                    |
| Generator Reactive Power| Sum of Max                | 0.28                    |
|                         | Sum of Min                | 1.12                    |
|                         | Sum of (Last – First)     | 27.73                   |
|                         | Sum of (Max – Min)        | 0.43                    |
|                         | Sum of Curve Area         | 1.16                    |
|                         | Sum of Curve Deviation    | 11.58                   |
|                         | Sum of Standard Deviation | 0.28                    |
| Generator Rotor Angle   | Sum of Max                | 2.06                    |
|                         | Sum of Min                | 16.60                   |
|                         | Sum of (Last – First)     | 10.54                   |
|                         | Sum of (Max – Min)        | 2.17                    |
|                         | Sum of Curve Area         | 3.67                    |
|                         | Sum of Curve Deviation    | 1.56                    |
|                         | Sum of Standard Deviation | 2.10                    |
| Line Active Power       | Sum of Max                | 1.55                    |
|                         | Sum of Min                | 0.34                    |
|                         | Sum of (Last – First)     | 3.71                    |
|                         | Sum of (Max – Min)        | 0.26                    |
|                         | Sum of Curve Area         | 2.37                    |
|                         | Sum of Curve Deviation    | 9.90                    |
|                         | Sum of Standard Deviation | 0.59                    |
| Line Reactive Power     | Sum of Max                | 3.51                    |
|                         | Sum of Min                | 9.39                    |
|                         | Sum of (Last – First)     | 11.43                   |
|                         | Sum of (Max – Min)        | 3.88                    |
|                         | Sum of Curve Area         | 0.77                    |
|                         | Sum of Curve Deviation    | 25.77                   |
|                         | Sum of Standard Deviation | 0.55                    |
| Bus Voltage             | Sum of Max                | 1.89                    |
|                         | Sum of Min                | 0.39                    |
|                         | Sum of (Last – First)     | 17.73                   |
|                         | Sum of (Max – Min)        | 1.23                    |
|                         | Sum of Curve Area         | 0.10                    |
|                         | Sum of Curve Deviation    | 21.95                   |
|                         | Sum of Standard Deviation | 0.19                    |
| Bus Frequency           | Sum of Max                | 0.99                    |
|                         | Sum of Min                | 0.63                    |
|                         | Sum of (Last – First)     | 37.02                   |
|                         | Sum of (Max – Min)        | 0.99                    |
|                         | Sum of Curve Area         | 1.28                    |
|                         | Sum of Curve Deviation    | 11.24                   |
|                         | Sum of Standard Deviation | 1.45                    |
| Bus Angle               | Sum of Max                | 9.55                    |
|                         | Sum of Min                | 20.56                   |
|                         | Sum of (Last – First)     | 40.27                   |
|                         | Sum of (Max – Min)        | 7.74                    |
|                         | Sum of Curve Area         | 13.15                   |
|                         | Sum of Curve Deviation    | 4.41                    |
|                         | Sum of Standard Deviation | 14.49                   |
| Interface Active Power  | Sum of Max                | 2.58                    |
|                         | Sum of Min                | 0.17                    |
|                         | Sum of (Last – First)     | 5.05                    |
|                         | Sum of (Max – Min)        | 0.42                    |
|                         | Sum of Curve Area         | 1.87                    |
|                         | Sum of Curve Deviation    | 10.33                   |
|                         | Sum of Standard Deviation | 0.24                    |
| Interface Reactive Power| Sum of Max                | 4.89                    |
|                         | Sum of Min                | 8.83                    |
|                         | Sum of (Last – First)     | 12.86                   |
|                         | Sum of (Max – Min)        | 4.65                    |
|                         | Sum of Curve Area         | 0.40                    |
|                         | Sum of Curve Deviation    | 28.60                   |
|                         | Sum of Standard Deviation | 0.67                    |
