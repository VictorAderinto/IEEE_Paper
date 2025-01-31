# Determining Relative Fault Severity for Real Time Transient Stability Analysis
## Overview of Metrics

During transient stability simulation, power system study engineers typically record various parameters such as terminal bus voltage, generator angle, line real and reactive power, and bus frequency at each time step. Figure 1 shows simulated voltage recorded during a simulation for a given contingency. The authors use this data to develop the severity metric described in the paper [1]. It is critical that these values are observed across the entire study area for accurate results. For example, if all the monitored buses are clustered around a subregion of the system, then it is likely that any metric devised would be biased to show higher severity for faults near that region and will likely not reflect broad system impacts, instead only representing local impacts. Therefore, to provide an unbiased view of the present state of the system, the monitored values must be evenly distributed across the entire study area. For this reason, parameters associated with components only sparsely available throughout the system were excluded from further analysis. Static VAr compensators are an example of such data excluded. The quantities which are broadly available throughout the system and selected for further analysis are given below:

* Generator active and reactive power, rotor angle 
* Line active and reactive power
* Bus voltage, frequency, and angle 
* Interface active and reactive power 



<p align="center">
  <img src="https://github.com/VictorAderinto/IEEE_Paper/blob/main/Quantity%20Measurement.png" alt="Bus Voltage Simulation Data" width="500"/>
  <br>
  <b>Figure 1: Simulation Measurements</b>
</p>

During the second phase of the analysis, the following seven metrics were calculated for each selected quantity:

* Sum of Max  
* Sum of Min 
* Sum of (Max-Min) 
* Sum of (Last Value - First value) 
* Sum of Curve Area  
* Sum of Curve Deviation 
* Sum of Standard Deviation  

To further illustrate the above calculations, assume that Figure 2 below shows one of the recorded quantities (let’s say voltage of a bus, for example). The calculation of the above metrics for this curve is explained in the next section. 

<p align="center">
  <img src="https://github.com/VictorAderinto/IEEE_Paper/blob/main/Sample%20Graph.png" width="400"/>
  <br>
  <b>Figure 2: Sample Data</b>
</p>


* **Sum of Max**: From the above plot, the maximum value (bus voltage) recorded was 0.44. Similarly, we can get the maximum value for all the other measurements (bus voltages in this example). The sum of the max is the summation of these maximum values.
* **Sum of Min**: The minimum value recorded in the above example was 0.25. Sum of Min is the summation of all the minimum values across all other measurements for that quantity.
* **Sum of (Max - Min)**: From the above graph, the difference between the maximum and minimum values is 0.19 (0.44 - 0.25). The sum of Max - Min is the summation of this value across all other measurements for that quantity.
* **Sum of (Last Value - First Value)**: The last value recorded in the above example was 0.34 and the first value recorded was 0.35. Therefore, the difference between the last value and first value is -0.01 (0.34 - 0.35). The sum of last value - first value is the summation of this value across all other measurements for that quantity.
* **Sum of Curve Area**: The sum of the absolute value of the area between the line and the curve is found using the equation below. This value is calculated and summed across all measurements for that quantity.

 $$ \text{Curve Area} = \frac{1}{N} \sum_{i=1}^{N} (Y_{\text{1}} - Y_i)^2 $$
  
  where `Y_1` is the first value in the curve, `Y_i` is the `i`-th value in the curve, and `N` is the number of discrete values in the curve.

* **Sum of Curve Deviation**: For each measurement, the difference between consecutive values is squared, summed together, and averaged, i.e., 1/N (Y1 - Y2)^2 + (Y2 - Y3)^2 + ⋯. From the sample graph this would be (0.35-0.25)^2 + (0.25 - 0.36) ^2 + (0.36 - 0.377) ^2 ...This value is determined for all the measurements for that quantity and then summed together.
* **Sum of Standard Deviation**: Sum of the standard deviation across all measurements for a quantity.

 $$ \text{Sum of Standard Deviation} = \sum_{i=1}^{N} \sigma_i $$


  where `σ_i` is the standard deviation of the `i`-th measurement and `N` is the total number of measurements.

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


## References

1.	Aderinto V., Beaudoin C., Wijeweera G., “Determining Relative Fault Severity for Real Time Transient Stability Analysis” submitted for IEEE PES general meeting 2025. 
