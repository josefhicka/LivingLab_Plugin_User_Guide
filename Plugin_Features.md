(Plugin_Features)=

# Plugin Features

This chapter deals with the functions of the plugin and how to use them. The SIMULTAN *LivingLab-Plugin* offers many possibilities (see {numref}`livinglab_functions`) and a customized UI.

```{figure} img/LivingLab_Functions.png
---
name: livinglab_functions
---
Overview of all functions within the *LivingLab-Plugin*
```

As you can see, the plugin includes a wide range of functions. Since we don't want to set any limits for the user and at the same time want to keep the user-friendliness quite high, there is a separate button for each feature.

```{note}
In the next revision of the plugin, the `Download Model` button will be removed, as it no longer serves any purpose or adds any value to the Plugin.
``` 

## Run Workflow 

The workflow button is the heart of the *LivingLab-Plugin*. It combines virtually all of the plugin's tools in a single function.

After opening the workflow button, you should see the following UI {numref}`RunWorkflwo_UI`:

```{figure} img/RunWorkflow_UI.png
---
name: RunWorkflwo_UI
---
UI for Running a Worklow in the LivingLab-Plugin
```

### Config File Path

A .config file is, as the name suggests, a configuration file. It typically contains settings and parameters that control the behavior of programs or systems. In our case, the file contains the API username, API password, and a link to the sensors so that the workflow can function smoothly.
The file can be found in the folder of the respective SIMULTAN file.

```{Tip}
If you cannot find your SIMULTAN file folder, for Windows you must enable the Hidden Objects option in the Explorer.
```

### Excution Mode
Excution Mode offers users two options:  
- **Continuous:** The interval can be defined in the *.config file* > ...<!-- Information von Zsombor wo Intervall im .config File definiert wurde--> `Number of Runs` specifies how often the simulation should be repeated.  
**Tip: -1 is the key for permanent repetition of the simulation.**
- **Specific Range:** Filling in the `Simulation Start` and `Simulation End` fields defines a time span for the simulation.


### Running the Workflow

**Starting the Simulation:**  
Based on the defined time window, the API can now retrieve the corresponding weather data and the sensor data from the LivingLab. The model is automatically exported to IDA-ICE. Instead of the standard data used in normal IDA-ICE simulations, the actual weather and sensor data measured and downloaded from the API is used as the framework conditions. The data is stored within the SIMULTAN components. Taxonomies enable the data to be uniquely identified by IDA-ICE. Finally, an IDA-ICE simulation is performed fully automatically.

The simulation results of the workflow function are therefore much more meaningful than those of normal simulations, and with the help of the LivingLab UI, you can be done in just a few minutes.

## Query and Persist Weather Data

The Query and Persist Weather Data button is used to get real weather data via an API connection into your SIMULTAN data model. The workflow function therefore includes this button. However, if you only want to integrate weather data for a specific period into your SIMULTAN file without directly starting an IDA-ICE simulation, this button is ideal.


### API Access

```{figure} img/APIAccess_UI.png
---
name: APIAccess_UI
---
UI for connecting to the API
```

In order to access weather data, you first need to establish a connection to the API (see {numref}`APIAccess_UI`). You can do this by adding the password. This can be found in the .config file > **“ApiPassword”:**.  
To check whether the connection has been established, press `Test Connection`.  
If everything has been successful, the message “Connection successful” should appear under the `Test Connection Button`.


### Datapoints

```{figure} img/Mapping_UI.png
---
name: Mapping_UI
---
UI for assigning sensors to values
```

In this area {numref}`Mapping_UI`, you can manually assign any sensor to each value. However, you need the exact key (the name of the sensor) for this, otherwise no corresponding results will be delivered. This allows users to determine for themselves which sensors reflect their data.

### Query

```{figure} img/Weather_Data_UI.png
---
name: Weather_Data_UI
---
UI for Query and Persist Weather Data
```

Before starting the simulation, you can again limit the simulation results to a specific time period. If the check mark is deactivated, the user has the option of specifying the time period in the `Start Date` and `End Date` fields ({numref}`Weather_Data_UI`). <!-- Frage an Andreas, ob die check-box wirklich diese Aufgabe hat?-->

### Results

```{figure} img/pos_SensorData.png
---
name: pos_SensorData
---
Positioning of sensor data within the ComponentBuilder
```

After starting the simulation, all data is saved within a very short time. This can be found within the *ComponentBuilder* > `Sensors` > `Weather Station` > `Diffusive Radiation` (see {numref}`pos_SensorData`).
This component consists of two subcomponents named `Sensor Data`.  
Both have different properties. One displays the data in a **table** and the other in a **graph**. The icons on the left edge of the component indicate the type of data representation involved.  
To enter on of both views, you must search for the Value section within the *PropertyEditor*. Click on the interactive text there, as shown in {numref}`PropertyEditor_graph`.

```{Tip}
If *PropertyEditor* is not enabled, you can enable it under the General tab.
```

```{figure} img/PropertyEditor_graph.png
---
name: PropertyEditor_graph
---
Illustration of the PropertyEditor
```

## IDA-ICE Export

This button causes the SIMULTAN model to be exported to IDA-ICE. The key difference is that SIMULTAN also automatically exports the measured weather data stored in the LivingLab components.

```{Note}
If you want to run an IDA-ICE simulation but don't necessarily need the weather data for your simulation, we don't recommend exporting the model via the LivingLab plugin. This is because the simulation with real weather data does not contain smooth functions and is therefore much more complex and slower than the standard simulation.
```