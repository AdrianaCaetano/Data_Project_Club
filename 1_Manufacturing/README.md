# MANUFACTURING OIL RIG

The first project is for an Industrial Manufacturing Company, which ficticious name is EnergyMobil.

Your role is to provide value to the company using the provided data to run the manufacturing plant more efficiently. 

### Data Analyst role
Create a manufacturing monitoring dasboard tht allows management to understand the manufacturing process in more detail.

### Dataset
The data comes from a real hydraulic rig system. This hydraulic rig is used to drill oil out of the ground. 

It has four main controls:
- the cooler setting
- the valve setting
- the pump seetting
- the accumulator setting

The rig has sensors in differenct areas measuring the pressure, volumetric flows, and temperatures. 


The original dataset is from [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/machine-learning-databases/00447/). A combined dataset is provided at [AveryData Github page](https://github.com/AveryData/hp-pred), [HourlyData.csv](https://github.com/AveryData/hp-pred/blob/main/HourlyData.csv) file. 

### Analysis

The data analysis was done on Google Colab using Python with Pandas, Matplotlib, Seaborn, and Skit-learn. The notebook is in the 1_Manufacturing folder.

After importing and analysing the data, I created some graphs to understnd how each feature behaved over time
![Plots of features](images/time_cool_motor_vol.png)
![Plots of features](images/temp_vibr_effic.png)
![Plots of features](images/pressure.png)

Then I created a coorelation matrix to check how features correlate to each other
![Correlation matrix](images/correlation_matrix.png)

Analysing the matrix, we can note that there is perfect positive correlation between :
- Temperature 1,2,3 and 4
- pressure bar 1 and 2
- Pressure bar 5 and 6 

also there is a perfect negative correlation between:
- Volume flow l/min 2 and temperature 3

And the features that have the greater impact on the Effective factor are:
- pressure bar 1 and 2

**But how the other correlations may affect the efficiency?**

To answeer this question, I created a list with all correlations above +-0.7 and created plots to visualize how these pairs affect the efficiency of the system. 
The graphs can clearly show that the system is affected when the following sensors reach the cited thresholds:

    Cooling efficiency < 25 and Motor power W > 2800
                            and Pressure bar 3 < 1
    Cooling power < 1.75 and Motor power W > 2500
                         and Pressure bar 3 < 1.5
    Motor power > 2500 and Pressure bar 1 > 160
                       and Pressure bar 2 > 130
    Pressure bar 1 > 160 and Pressure bar 2 > 130
    Vibration >= 0.8 and Pressure bar 3 < 1.5
 
This is an example of a scatter plot showing how the correlated features affects the efficiency.
![Cooling efficiency vs Motor power](images/cooling_efficiency_motor_power.png)


### Dashboard

After the analysis, a dashboard was created to monitor the system. 

### References

This is the summary from the UCI database files `description.txt` and `documentation.txt`:

**Relevant Information:**

The data set was experimentally obtained with a hydraulic test rig. This test rig consists of a primary working and a secondary cooling-filtration circuit which are connected via the oil tank. The system cyclically repeats constant load cycles (duration 60 seconds) and measures process values such as pressures, volume flows and temperatures while the condition of four hydraulic components (cooler, valve, pump and accumulator) is quantitatively varied.

**Number of Instances:** 2205

**Number of Attributes:** 43680 (8x60 (1 Hz) + 2x600 (10 Hz) + 7x6000 (100 Hz))

**Attribute Information:**

- Attributes are sensor data (all numeric and continuous) from measurements taken at the same point in time, respectively, of a hydraulic test rig's working cycle.
- The sensors were read with different sampling rates, leading to different numbers of attributes per sensor despite they were all exposed to the same working cycle.
   
   1. Pressure sensors (PS1-6): 100 Hz, 6000 attributes per sensor (6 sensors)
   2. Motor power sensor (EPS1): 100 Hz, 6000 attributes per sensor (1 sensor)
   3. Volume flow sensors (FS1/2): 10 Hz, 600 attributes per sensor (2 sensors)
   4. Temperature sensors (TS1-4): 1 Hz, 60 attributes per sensor (4 sensors)
   5. Vibration sensor (VS1): 1 Hz, 60 attributes per sensor (1 sensor)
   6. Efficiency factor (SE): 1 Hz, 60 attributes per sensor (1 sensor)
   7. Virtual cooling efficiency sensor (CE): 1 Hz, 60 attributes per sensor (1 sensor)
   8. Virtual cooling power sensor (CP): 1 Hz, 60 attributes per sensor (1 sensor)


**Missing Attribute Values:** None

**Attribute Information:** 

The data set contains raw process sensor data with the rows representing the cycles and the columns the data points within a cycle. The sensors involved are:

Sensor	|	Physical quantity	|	Unit	|	Sampling rate
--------|-----------------------|-----------|-----------------
PS1	|	Pressure	|		bar	|	100 Hz
PS2	|	Pressure	|		bar	|	100 Hz
PS3	|	Pressure	|		bar	|	100 Hz
PS4	|	Pressure	|		bar	|	100 Hz
PS5	|	Pressure	|		bar	|	100 Hz
PS6	|	Pressure	|		bar	|	100 Hz
EPS1	|	Motor power		|	W	|	100 Hz
FS1	|	Volume flow		|	l/min	|	10 Hz
FS2	|	Volume flow		|	l/min	|	10 Hz
TS1	|	Temperature		|	∞C	|	1 Hz
TS2	|	Temperature		|	∞C	|	1 Hz
TS3	|	Temperature		|	∞C	|	1 Hz
TS4	|	Temperature		|	∞C	|	1 Hz
VS1	|	Vibration		|	mm/s	|	1 Hz
CE	|	Cooling efficiency (virtual)|	%	|	1 Hz
CP	|	Cooling power (virtual)	|	kW	|	1 Hz
SE	|	Efficiency factor	|	%	|	1 Hz

### Diagram of the System

![Oil Rig System Diagram](images/oil_rig_diagram.png)

Source: Alenany, A., Helmi, A. M., & Nasef, B. M. (2021). Comprehensive Analysis for Sensor-based Hydraulic System Condition Monitoring. International Journal of Advanced Computer Science and Applications, 12(6), 153-162.
