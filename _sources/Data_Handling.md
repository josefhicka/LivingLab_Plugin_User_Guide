(Data_Handling)=

# Data Handling

This chapter focuses on managing and retrieving data within the *LivingLab Plugin*. You will learn how to query and persist weather data from the API, map sensor keys to parameters, and manage raw and processed sensor datasets. Clear guidance is provided on input requirements, UI usage, and storage within the SIMULTAN data model.

---

## Query and Persist Weather Data

The `Query and Persist Weather Data` feature retrieves weather data from the API and stores it in the SIMULTAN data model. The Workflow includes this step; use this button when you want to import weather data for a specific period without immediately running the entire workflow.

**The UI is divided into three parts, which are divided into tabs:**  
[API Access](#api-access) > All API-related information relevant to establishing a connection.  
[Datapoints](#datapoints) > Individual assignment of sensors to weather parameters.   
[Query](#query) > Selection of a period from which the weather data is obtained.  

### API Access

```{figure} img/APIAccess_UI.png
---
name: APIAccess_UI
---
UI for connecting to the API
```

{numref}`APIAccess_UI` To access weather data, establish a connection to the API by adding the API password (stored in the `config` file). Use `Test Connection` to verify connectivity. On success, the UI displays **“Connection successful”** below the test button.

> More about the `config` file [here](Workflow.md#config-file-path)

---

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

Use the `Start Date` and `End Date` fields to limit the imported weather data to a specific time range. If the checkbox `Use Simulation Data Range` is enabled the plugin uses the time stamps defined in the Simulation Data. *ComponentBuilder* > `IDA ICE Analysis` > `Simulation Data` > `Warmup Phase`.

### Results

```{figure} img/pos_SensorData.png
---
name: pos_SensorData
---
Positioning of sensor data within the ComponentBuilder
```

Imported data is stored in dedicated components. For example under *ComponentBuilder* > `Sensors` > `Weather Station` > `Diffusive Radiation` (see {numref}`pos_SensorData`).
The component contains two subcomponents named `Sensor Data` — one shows a table, the other a graph. Icons to the left of each subcomponent indicate the representation type.

To open either view, locate the Value section in the *PropertyEditor* and click the interactive text (see {numref}`PropertyEditor_graph`).

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

- [Download Raw Sensor Data](#download-sensor-data-raw-processed)
- [Download Processed Sensor Data](#download-sensor-data-raw-processed)
- [Extract Sensor Data from SIMULTAN](#extract-sensor-data-from-simultan)

---

```{note}
To ensure that the sensor data is processed smoothly, please ensure that CSV Importer uses the *English language standard* (**comma as separator** and **period as decimal separator**). Otherwise, problems arise when opening the converted data, resulting in an unclean CSV file.
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

### Extract Sensor Data from SIMULTAN

{numref}`extract_sensordata` This function allows you to download data based on a specific component. This allows you to save the current status of your data from your SIMULTAN data model separately. As a **backup** or for other purposes.

```{figure} img/extract_sensordata.png
---
name: extract_sensordata
---
UI for the function Extract Sensor Data from SIMULTAN
```

#### How to use

1. Click *Extract Sensor Data from SIMULTAN*
2. Enter the taxonomy from which you want to extract the data. (e.g., **Temperature_Sensor_Weather**  |  You can find the taxonomy under the following components: `Sensors` > `Weather Station` > `Temperature Air`)
3. Press *Extract* 
4. Save the data in your file directory.

---

*After retrieving and mapping sensor and weather data, it is crucial to ensure that time formats are consistent. The next chapter, Time Handling, explains how to convert and standardize your datasets for further processing.*