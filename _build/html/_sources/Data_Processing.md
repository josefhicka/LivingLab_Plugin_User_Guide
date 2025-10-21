(Data_Processing)=

# Data Processing

Once data has been retrieved and time formats standardized, it needs to be processed for comparison and analysis. This chapter covers steps to clean, average, and align sensor data with simulation results, allowing for accurate validation and seamless integration of real-world and simulated data.

---

## Process Data Points for Comparison

The **Process Data Points for Comparison** button converts raw CSV sensor data into a cleaned format suitable for direct comparison with simulation result CSV files.  

It processes CSV files containing sensor data in two possible formats:  

- **Timestamps (DateTime)**  
- **Hour indices**  

### Processing steps

1. Averages multiple readings within the same hour.  
2. Converts timestamps into hour indices based on the specified year.  
3. Fills missing hours by estimating values between available data points.  

### Output

The output is a cleaned CSV file with two columns:  

- **Hour index** (0–8759)  
- **Corresponding sensor value**  

<!-- Beispiel csv anfügen!-->

---

## Add Control Data to Simulated Results

The **Add Control Data to Simulated Results** button merges real-world sensor data with simulation outputs, enabling side-by-side comparison of predicted and actual building performance.  

### Prerequisites

**Simulation Data:**
- The simulation data file must be a `.prn` file (an IDA-ICE simulation result) converted into a CSV format. Use [Convert Temperature Files](IDAICE_Integration.md#convert-temperature-files) to perform this conversion.
- The resulting simulation CSV file must include clearly named columns, typically `Mean Temperature` and `Operative Temperature`.   

**Controll Data:**
- The control data must be provided as a CSV file containing a simple hourly indexed list of values.

---

>  The function can also compare files with different numbers of data points or varying time intervals.
However, it aligns values based on the hourly indices of the target CSV file, to which the control data is added.



### How it works

1. Select a **control data CSV file** containing hourly indexed sensor data.  
2. Specify the **name of the new column** where control values will be stored.  
3. Choose the **target simulation CSV file with hourly index**.  
4. The tool matches records by **hour index** and appends the corresponding control sensor values as a new column.  

### Output

The selected simulation CSV file is updated *in place*.  
- All existing simulation data is preserved.  
- The real-world control data is integrated as an additional column for direct comparison. 

---

## Simulate and Process Results

The **Simulate and Process Results** button automates the entire building validation workflow. It integrates simulation and measurement data into a single process — from running IDA-ICE simulations to producing a unified CSV file for comparing predicted and actual building performance.  

### Automated pipeline steps

1. Launches **IDA-ICE** and simulates the selected IDA-ICE model (.idm file).  
2. Extracts **temperature results** from the simulation output files.  
3. Retrieves the **simulation dates** from the model to define the data query period.  
4. Downloads **real sensor data** from the LivingLab API for the exact timeframe.  
5. Processes both datasets into **hourly averages**, including gap-filling where needed.  
6. Merges simulation and sensor data by matching **hour indices**.  
7. Outputs a **unified CSV file** containing both predicted and measured values side-by-side.  

### Input fiels

```{figure} img/simandprocessresults.png
---
name: simandprocessresults
---
Simulate and Process Results UI and Input fields
```

**Input fields explained** ({numref}`simandprocessresults`)
- **Model File Path** — IDA-ICE model as the baseline for comparison.
- **Name Of Simulation Room** — path to the standalone command-line version of the IDA-ICE-Plugin.
- **Idaice Path** — the path to the IDA-ICE executable (e.g., C:\Program Files\IDA-ICE\bin\ida-ice.exe).
- **Idaice Exporter Path** — selects the sensor/key to download.
- **API** — username, password, and URL for linking the API.
- **Project Id** — required by the Aedifion API.
- **Control DataPoint Id** — selects the sensor/key for comparison.

### Output

The result is a single CSV file in which:  
- Simulation results (predicted values) and real sensor data (measured values) are aligned **by hour index**.  
- The dataset is ready for direct validation, visualization, or further analysis.  

```{note}
This function replaces multiple manual steps with one automated workflow. Ensure that both the simulation model and API credentials are correctly configured before running the process.
```

---

*After processing and aligning all sensor and simulation data, the next step is to integrate these datasets with IDA-ICE. The following chapter, **IDA-ICE Integration**, guides you through exporting SIMULTAN models to IDA-ICE, running simulations, and importing the results back for further analysis and validation.*