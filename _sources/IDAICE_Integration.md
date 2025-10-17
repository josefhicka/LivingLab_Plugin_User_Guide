(IDAICE_Integration)=

<!-- Update Simultation Data hinzufügen!-->

# IDAICE Integration

This chapter covers all functions of the *LivingLab plugin* that relate to data transfer between IDA-ICE and SIMULTAN: **IDA-ICE Export**, **IDA-ICE Simulate**, and **IDA-ICE Import Results**. Each feature is available via its own button in the LivingLab UI and is intended to support an end-to-end workflow: export a SIMULTAN model to an IDA-ICE model file (.idm), run IDA-ICE simulations, and import the resulting results back into SIMULTAN.

---

## IDA-ICE Export

The **IDA-ICE Export** button converts the active SIMULTAN Datamodel into an IDA-ICE model files (.idm). The export converts geometry (including zones and shading elements), constructions, material properties, and the ESBO plant  from the SIMULTAN data model into an IDA-ICE file.

```{Note}
Exporting the SIMULTAN model using the LivingLab plugin means that all measured data is also exported. Causing less smooth, more complex, and slower simulations. If this measured data is not needed, you can avoid the disadvantage by using the export function of the IDA-ICE plugin. 
```

---

### How to use

1. Click IDA-ICE Export
2. Name the file
3. Save as an idm. file

<!-- Eventuell rausgeben da es überflüssig ist, selbsterklärend!-->

---

## IDA-ICE Simulate

The **IDA-ICE Simulate** button launches IDA-ICE to run simulations using selected .idm model files. The plugin starts IDA-ICE, monitors the external process, and reports completion and basic status to the user. Typical simulation outputs are text-based result files such as TEMPERATURES.prn, ZONE-ENERGY.prn, and ENERGY.prn.

```{figure} img/IDAICE_Simulate.png
---
name: IDAICE_Simulate
---
UI for the IDA-ICE Simulate Button
```
---

### How to use

1. Click IDA-ICE Simulate.
2. In the dialog, specify the path to the IDA-ICE executable (e.g., C:\Program Files\IDA-ICE\bin\ida-ice.exe (see {numref}`IDAICE_Simulate`)).
3. Click Simulate, then select the .idm file you want to run.
4. The plugin launches IDA-ICE and polls the ida-ice process every 5 seconds to monitor progress.
5. When the process is complete, the simulation generates standard result files (TEMPERATURES.prn, ENERGY.prn, etc.).

<!-- Bild von ausgegeben Dateien!-->


---

## IDA-ICE Import Results

The **IDA-ICE Import Results** button reads IDA-ICE simulation output files and transfers the results back into the SIMULTAN data model. The import parses per-room result files and creates or updates components that contain time-series data (tables and graphs) for heating loads, cooling loads and operative temperatures.

---

### How it works

1. Click IDA-ICE Import Results and select the corresponding .idm result file (of one specific room).
2. The plugin iterates over all rooms defined in SIMULTAN under the Roomlist component. For each zone it searches the simulation output folder and subfolders for matching result files (e.g., ZONE-ENERGY.prn, TEMPERATURES.prn).
3. For each room found, the plugin parses the relevant files: heating/cooling loads from ZONE-ENERGY.prn, temperatures from TEMPERATURES.prn. 
4. Within SIMULTAN these files get stored under the components: `IDA ICE Analyses` > `Results`. Time series are stored as both table and graph parameters.

### Expected result structure

<!-- Verweis auf ergebnisse, und alles was dabei wichtig ist!-->
<!-- If there are results, then those get imported under the IDA ICE Analysis/Results component. Also, you can see the new Tables and Graphs added under the Value Fields tab in Simultan. -->


## Update Simulation Data

This function updates the simulation and warm-up dates in the current SIMULTAN project.
The corresponding components are located in the *ComponentBuilder* under `LivingLab` > `IDAICEAnalysis` > `Simulation Data` (see {numref}`simulationdata_components`).
When executed, these components are exported into the IDA-ICE model file, ensuring that the simulation runs over the correct time interval.

```{figure} img/simulationdata_components.png
---
name: simulationdata_components
---
Update Simulation Data Components
```

###  How to use

1. Click on `Update Simulation Data` to open the function ({numref}`updatesimdata_ui`).
2. The UI includes 3 parameters; `Warmup Start` `Simulation Start` `Simulation End`.
3. Enter these three parameters in ascending order, using the following format: `yyyy-mm-dd hh:mm:ss` (e.g., `2025-10-17 15:37:00`).
4. Confirm with `Close`.

```{figure} img/updatesimdata_ui.png
---
name: updatesimdata_ui
---
Update Simulation Data UI
```

```{note}
The `Simulation Start` parameter represents both the **End Date** of the `Warmup Phase` and the **Start Date** of the `Simulation Phase`, as these two phases are directly linked.
``` 