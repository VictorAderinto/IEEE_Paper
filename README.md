<h1 align="center">
  Determining Relative Fault Severity for Real Time Transient Stability Analysis
</h1>


<p align="center">
  Victor Aderinto, Chris Beaudoin, Gayan Wijeweera<br>
Manitoba Hydro <br>
Winnipeg, Canada
</p>


## Proposed Metrics

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


* **Sum of Max**: From the above plot, the maximum value (bus voltage) recorded was `0.44`. Similarly, we can get the maximum value for all the other measurements (bus voltages in this example). The sum of the max is the summation of these maximum values.
* **Sum of Min**: The minimum value recorded in the above example was `0.25`. Sum of Min is the summation of all the minimum values across all other measurements for that quantity.
* **Sum of (Max - Min)**: From the above graph, the difference between the maximum and minimum values is `0.19 (0.44 - 0.25)`. The sum of Max - Min is the summation of this value across all other measurements for that quantity.
* **Sum of (Last Value - First Value)**: The last value recorded in the above example was `0.34` and the first value recorded was `0.35`. Therefore, the difference between the last value and first value is `-0.01 (0.34 - 0.35)`. The sum of last value - first value is the summation of this value across all other measurements for that quantity.
* **Sum of Curve Area**: The sum of the absolute value of the area between the line and the curve is found using the equation below. This value is calculated and summed across all measurements for that quantity.

 $$ \text{Curve Area} = \frac{1}{N} \sum_{i=1}^{N} abs(Y_{\text{1}} - Y_i) $$
  
  where `Y_1` is the first value in the curve, `Y_i` is the `i`-th value in the curve, and `N` is the number of discrete values in the curve.

* **Sum of Curve Deviation**: For each measurement, the difference between consecutive values is squared, summed together, and averaged, i.e., `1/N ∑ (Y_1 - Y_2)^2 + (Y_2 - Y_3)^2 + ...`. From the sample graph, this would be `(0.35 - 0.25)^2 + (0.25 - 0.36)^2 + (0.36 - 0.377)^2 + ...`. This value is determined for all the measurements for that quantity and then summed together.
  
* **Sum of Standard Deviation**: Sum of the standard deviation across all measurements for a quantity.

 $$ \text{Sum of Standard Deviation} = \sum_{i=1}^{N} \sigma_i $$


  where `σ_i` is the standard deviation of the `i`-th measurement and `N` is the total number of measurements.

## Metric Evaluation
The above metrics were calculated for each power system quantity and an aggregrate ranking error was derived to demonstrate correlation with severity, where lower value implies higher correlation. The aggregate ranking error is derived as follows:
* We establish a direct relationship between severity and clearing time.
* With this relationship established, we design a test simulation with 21 different faults, each with 8 clearing times of increasing magnitude.
* We utilize the metrics to rank all faults. Given that severity is directly related to clearing time, the ideal metric should rank each fault in order of clearing time, where `0 represents the lowest clearing time & severity and 7 the highest clearing time & severity`.
* The average ranking across all 21 faults is calculated for each metric, and the deviation from the ideal ranking `(which is [0, 1, 2, 3, 4, 5, 6, 7] or [7, 6, 5, 4, 3, 2, 1])` is determined.
* This deviation is the aggregate ranking error.

The metrics in Table 1 consist of measurements from over 260 generators for generator metrics (generator reactive power, generator active power, generator rotor angle), over 80 lines for line metrics (line active power, line reactive power), over 190 buses for bus metrics (bus voltage, bus frequency, bus angle) and 10 interface connections between Manitoba Hydro and other utilities. The results are summarized below:

<b>Table 1: Summary of Metric Evaluation</b>

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

## Broad System Benchmarking

From Table 1 above, the top 5 metrics most accurate at predicting at severity are: 
1.	bus voltage – curve_area
2.	interface power - min
3.	bus voltage – stdev
4.	interface power – stdev
5.	line active power - max – min

We replicated the methodology for developing the metrics, this time using power flows with various system loading conditions, prior outage scenarios, and interface transfer limits. The values in Table 2 represent the aggregrate ranking error given a system condition. If the above metrics consistently quantify severity across all these scenarios, we can confirm their effectiveness as severity quantifiers. The results are summarized in Table 2 below.

<b>Table 2: Summary of Broad System Benchmarking </b>

|Scenario        | bus_v – curve_area | iface_p - min | bus_v – stdev | iface_p – stdev | line_p - max – min |
|----------------|--------------------|---------------|---------------|-----------------|--------------------|
| Power Flow 1 | 0.145              | 3.125         | 0.32          | 0.37            | 0.55               |
| Power Flow 2 | 0.13               | 1.265         | 0.73          | 0.325           | 0.55               |
| Power Flow 3 | 0.23               | 0.22          | 0.41          | 0.985           | 0.34               |
| Power Flow 4 | 0.08               | 0.54          | 0.185         | 0.27            | 0.435              |
| Power Flow 5 | 0.14               | 0.175         | 0.3           | 0.43            | 0.44               |
| Power Flow 6 | 0.055              | 0.86          | 0.09          | 0.845           | 1.07               |
| Power Flow 7 | 0.3                | 1.47          | 0.7           | 1.04            | 0.745              |
| Power Flow 8 | 0.18               | 1.34          | 1.1           | 0.585           | 0.685              |
| Power Flow 9 | 0.11               | 0.655         | 0.15          | 0.855           | 0.675              |
| **Avg Deviation**  | **0.152**            | 1.072         | 0.443         | 0.634           | 0.61               |

For each of these system conditions, the bus voltage metric consistently ranked the lowest or one of the lowest, with an error of 0.01 for one of the system conditions and an average error of 0.152, showing its robustness across varying sytem conditions.

## Benchmarking against CCT

For further verification, sixteen faults were selected, labeled A through P, in a region with known stability issues. Five scenarios were prepared, each with a different fault close to the stability boundary. It follows that the fault nearest to instability should be ranked as the most severe. Both CCT and the proposed metric were used to rank the faults and the results are summarized in Table 3 below.

For each scenario, Table 3 identifies the contingency closest to the stability boundary and provides the complete rankings of all 16 faults, from most severe to least severe, according to both the metric and CCT.

<b>Table 3: Summary of Benchmarking against CCT</b>

| Scenario #    | Critical Ctgy       | Metric Ranking | CCT Ranking |
|--------------|-------------------|----------------|-------------|
| 1 | A                    | A, N, P, C, E, K, L, J, D, B, M, G, O, F, H, I | A, N, K, C, E, L, J, P, D, G, B, O, H, M, I, F |
|  2 | M                    | M, F, P, E, C, K, L, H, J, D, G, O, B, N, I, A | M, K, E, C, L, P, H, J, D, A, F, G, I, B, N, O |
|  3 | B                    | B, D, G, L, K, C, O, P, E, J, H, A, N, M, F, I | B, D, G, L, K, O, P, E, J, C, A, N, M, I, F, H |
|  4 | E                   | E, A, P, K, D, B, L, C, H, G, J, M, O, F, I, N | E, L, C, A, D, K, J, G, P, B, O, M, H, F, I, N |
|  5 | N                    | N, A, O, K, B, H, P, D, L, G, E, C, M, J, F, I | N, K, B, D, L, G, P, C, A, O, E, J, M, F, I, H |

As seen above, the proposed metric and CCT both correctly select the fault nearest to instability as the most severe fault in every test case. The remaining 15 faults are somewhat consistently ranked. The computation time required to calculate CCT for these 16 faults was approximately 200 minutes per scenario compared to approximately 20 minutes for the proposed metric.

## References

1.	Aderinto V., Beaudoin C., Wijeweera G., “Determining Relative Fault Severity for Real Time Transient Stability Analysis” submitted for IEEE PES general meeting 2025. 
