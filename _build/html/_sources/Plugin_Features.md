(Plugin_Features)=

# Plugin Features

This chapter describes the plugin’s functions and explains how to use them. The SIMULTAN *LivingLab Plugin* provides a broad set of features and a tailored user interface.  

To maximise flexibility while keeping the interface user-friendly, each feature is exposed via a dedicated button.


```{warning}
In the next revision of the plugin, the `Download Model` button will be removed because it no longer provides value.
``` 

---

## Run Workflow 

The **Workflow** button is the core of the LivingLab Plugin. It combines nearly all plugin tools into a single, automated sequence from data retrieval to running an IDA-ICE simulation.

After opening the Workflow UI you should see the following screen {numref}`RunWorkflwo_UI`:

```{figure} img/RunWorkflow_UI.png
---
name: RunWorkflwo_UI
---
UI for Running a Worklow in the *LivingLab Plugin*
```

### Config File Path

 The `config` file (configuration file) contains settings that control the plugin behaviour. For this plugin the file typically includes the API username, API password, the sensor endpoint (or sensor mapping), and other parameters required by the workflow. The `config` file has to be stored in the same folder as the corresponding SIMULTAN file.


```{Tip}
If you cannot find your SIMULTAN file folder on Windows, enable "Hidden Objects" in File Explorer.
```

---

### Excution Mode
The Workflow supports two execution modes:
- **Continuous:**  
The interval for repeated runs is defined in the `config` file > ...<!-- Information von Zsombor wo Intervall im config File definiert wurde-->   
`Number of Runs` specifies how many times the simulation should repeat.   
**Tip:** Setting `Number of Runs = -1` triggers continuous, indefinite repetition.
- **Specific Range:**  
Define a concrete time window by filling the `Simulation Start` and `Simulation End` fields; the workflow runs only for this period.
<!-- ⚠️ Vorschlag: Dokumentieren Sie genau, welcher .config-Schlüssel das Intervall definiert (Name, Einheiten), und geben Sie eine Parameterbeschreibung an (z. B. Millisekunden, Sekunden, Minuten). -->

---

### Running the Workflow

**Starting the Simulation:**  
Given the configured `Execution Mode`, the plugin retrieves the corresponding weather and sensor data from the API.

**Simulationphase:**
The model is exported automatically to IDA-ICE. Instead of synthetic or standard boundary conditions, the workflow substitutes the measured weather and sensor data downloaded from the API as the boundary for the IDA-ICE simulation. Data required for clean exports are organised in SIMULTAN components and annotated with taxonomies so that IDA-ICE can uniquely identify them. Finally, the IDA-ICE simulation is started automatically.

**Results:**
Because the simulation uses measured input data, results from the workflow are typically more representative of real operation than standard simulations. Using the LivingLab UI, a full end-to-end run can be completed quickly.

## Query and Persist Weather Data

The `Query and Persist Weather Data` feature retrieves weather data from the API and stores it in the SIMULTAN data model. The Workflow includes this step; use this button when you want to import weather data for a specific period without immediately running an IDA-ICE simulation.

**The UI is divided into three parts, which are divided into tabs.**  
[API Access](#api-access) > connect to the API  
[Datapoints](#datapoints) > assign sensors  
[Query](#query) > select the time window  

### API Access

```{figure} img/APIAccess_UI.png
---
name: APIAccess_UI
---
UI for connecting to the API
```

{numref}`APIAccess_UI` To access weather data, establish a connection to the API by adding the API password (stored in the .config file). Use Test Connection to verify connectivity. On success, the UI displays “Connection successful” below the test button.

More about the `config` file [here](#config-file-path)

### Datapoints

```{figure} img/Mapping_UI.png
---
name: Mapping_UI
---
UI for assigning sensors to values
```

In this area ({numref}`Mapping_UI`) you manually map API sensor keys to the corresponding weather parameters. The mapping requires the exact sensor key (name) returned by the API; incorrect keys will produce no data. This mapping decides which sensor values populate which weather parameters in the SIMULTAN model.
<!-- verweis darauf wo die excakten sensor namen gefunden werden können!-->

### Query

```{figure} img/Weather_Data_UI.png
---
name: Weather_Data_UI
---
UI for Query and Persist Weather Data
```

Use the Start Date and End Date fields to limit the imported weather data to a specific time range. The checkbox `Use Simulation Data Range` in the user interface controls the use of the fields. Make sure that the checkbox is enabled before starting the query.

### Results

```{figure} img/pos_SensorData.png
---
name: pos_SensorData
---
Positioning of sensor data within the ComponentBuilder
```

Imported data is stored in dedicated components under *ComponentBuilder* > `Sensors` > `Weather Station` > `Diffusive Radiation` (see {numref}`pos_SensorData`).
The component contains two subcomponents named `Sensor Data` — one shows a table, the other a graph. Icons to the left of each subcomponent indicate the representation type.

To open either view, locate the Value section in the `PropertyEditor` and click the interactive text (see {numref}`PropertyEditor_graph`).

```{Tip}
To open the *PropertyEditor*: go to the General tab and click the *PropertyEditor* button — it appears on the right side of the screen.
```

```{figure} img/PropertyEditor_graph.png
---
name: PropertyEditor_graph
---
Illustration of the PropertyEditor
```

---

## Sensor Data

 SIMULTAN provides three integrated actions for manual sensor-data handling:

- [Download Raw Sensor Data](#download-sensor-data)
- [Download Processed Sensor Data](#download-sensor-data)
- [Extract Sensor Data from SIMULTAN](#extract-sensor-data-from-simultan)

---

```{note}
To ensure that the sensor data is processed smoothly, please ensure that CSV Importer uses the *English language standard* (**comma as separator** and **period as decimal separator**). Otherwise, problems may arise when when opening the converted data, resulting in an unclean CSV file.
``` 

---

### Download Sensor Data (raw & processed)

The buttons `Download Raw Sensor Data` and `Download Processed Sensor Data` work with the same user interface and are therefore identical to use.

```{figure} img/sensor_data_ui.png
---
name: sensor_data_ui
---
UI for downloading Sensor Data
```

**Input fields explained** ({numref}`sensor_data_ui`)
- **API Password** — required for authentication.
- **Start Date / End Date** — define the time window for the download.
- **DataPoint** — selects the sensor/key to download.
- **Zone Name** — the destination component/zone in the SIMULTAN data model where data will be stored.
- **Taxonomy** — a unique identifier assigned to the imported data for later export and mapping.

After filling the fields you can either download the data as a **CSV file** or integrate the data directly into the SIMULTAN data model (the Zone Name and Taxonomy fields are used in that case).

---

#### Raw vs Processed Sensor Data

Processed data differs from raw data primarily by smoothing and cleaning steps. The plugin offers both so users can choose between fidelity to the original measurements and easier-to-handle datasets.

| Attribute             | Raw Sensor Data                     | Processed Sensor Data                  |
|-----------------------|-------------------------------------|----------------------------------------|
| Data Size             | Very large                  | Smaller                        |
| Evaluation Effort     | High                        | Low                            |
| Error Susceptibility  | Contains outliers/noise     | Mostly cleaned                 |
| Data Granularity      | Maximum                     | Reduced                |

---

## Extract Sensor Data from SIMULTAN

{numref}`extract_sensordata` This function allows you to download data based on a specific component. This allows you to save the current status of your data from your SIMULTAN data model separately. As a backup or for other purposes.

```{figure} img/extract_sensordata.png
---
name: extract_sensordata
---
UI for the function Extract Sensor Data from SIMULTAN
```

### How to use

1. Click *Extract Sensor Data from SIMULTAN*
2. Enter the taxonomy from which you want to extract the data. (e.g., Temperature_Sensor_Weather | You can find the taxonomy under the following components: `Sensors` > `Weather Station` > `Temperature Air`)
3. Press *Extract* 
4. Save the data in your file directory.

---

## Time Format Conversion

`DateTime` and `HourlyIndex` formats are two common ways to represent time in datasets and simulations. `DateTime` includes full date and time information, making it easy to trace, compare, and interpret exact moments or periods. An `HourlyIndex`, on the other hand, simply counts each hourly interval from a defined starting point—this is useful for simulations and calculations that focus on time steps rather than specific dates.

Converting between these formats is important: it lets users switch easily between human-readable times and efficient index-based processing. The ability to convert ensures flexibility when working with data, helping match the needs of both calculations and presentation.

---

```{warning}
Check that all data records in your `.csv` file are formatted consistently. Just one outlier is enough to prevent a successful conversion.
``` 

---

### How to use

1. Press one of the two buttons, `Convert DateTime to Hourly Indexed` or `Convert Hourly Indexed to DateTime`, depending on what you want to do.
2. Specify the year of your data. <!-- WAs ist wenn die daten in mehreren jahren sind?-->
3. Press `Browse...` to select the file you want to convert.
4. Click `Convert` to start the process.

> {numref}`Index_Converter` Both functions/UI work exactly the same way, just make sure you use the right method based on your input data.

```{figure} img/Index_Converter.png
---
name: Index_Converter
---
UI for converting time indices
```

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
- **Project Id** — <!-- Zsombor fragen-->.
- **Control DataPoint Id** — selects the sensor/key for comparison.

### Output

The result is a single CSV file in which:  
- Simulation results (predicted values) and real sensor data (measured values) are aligned by hour index.  
- The dataset is ready for direct validation, visualization, or further analysis.  

```{note}
This function replaces multiple manual steps with one automated workflow. Ensure that both the simulation model and API credentials are correctly configured before running the process.
```