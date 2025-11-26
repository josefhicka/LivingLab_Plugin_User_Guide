(IDAICE_Integration)=


# IDAICE Integration

This chapter covers all functions of the *LivingLab Plugin* that relate to data transfer between IDA-ICE and SIMULTAN: IDA-ICE Export, IDA-ICE Simulate, IDA-ICE Import Results and more. Each feature is available via its own button in the LivingLab UI and is intended to support an end-to-end workflow: export a SIMULTAN model to an IDA-ICE model file (.idm), run IDA-ICE simulations, and import the resulting results back into SIMULTAN.

---

## IDA-ICE Export

The **IDA-ICE Export** button converts the active SIMULTAN Datamodel into an IDA-ICE model files (.idm). The export converts geometry (including zones and shading elements), constructions, material properties, and the ESBO plant  from the SIMULTAN data model into an IDA-ICE file.

---

```{Note}
Exporting the SIMULTAN model using the *LivingLab Plugin* means that all measured data is also exported. If this measured data is not needed, you can avoid the disadvantage by using the export function of the IDA-ICE plugin. 
```

---

### How to use

1. Click *IDA-ICE Export*
2. Name the file
3. Save as an `.idm` file


---

## IDA-ICE Simulate

The **IDA-ICE Simulate** button launches IDA-ICE to run simulations using selected .idm model files. The plugin starts IDA-ICE, monitors the external process, and reports completion and basic status to the user. Typical simulation outputs are text-based result files such as *TEMPERATURES.prn*, *ZONE-ENERGY.prn*, and *ENERGY.prn*.

```{figure} img/IDAICE_Simulate.png
---
name: IDAICE_Simulate
---
UI for the IDA-ICE Simulate Button
```
---

### How to use

1. **Click** *IDA-ICE Simulate*.
2. In the dialog, **specify the path to the IDA-ICE executable** (e.g., C:\Program Files\IDA-ICE\bin\ida-ice.exe (see {numref}`IDAICE_Simulate`)).
3. **Click Simulate**, then **select the .idm file** you want to run (created in [*IDA-ICE Export*](#ida-ice-export)).
4. The plugin launches IDA-ICE and polls the ida-ice process every 5 seconds to monitor progress.
5. When the process is complete, the simulation **generates standard result files** (TEMPERATURES.prn, ENERGY.prn, etc. (see {numref}`idaice_simulate_folder`)) in **the created folder** belonging to the simulated .idm file.

---

```{figure} img/idaice_simulate_folder.png
---
name: idaice_simulate_folder
---
Generated results files within the created folder
```
<!-- Bild nicht passend simulation hat keine unterordner erstellt!-->

---

## IDA-ICE Import Results

The **IDA-ICE Import Results** button reads IDA-ICE simulation files and transfers the simulated results back into the SIMULTAN data model. The import parses per-room result files and creates or updates components that contain time-series data (tables and graphs) for heating loads, cooling loads and operative temperatures.

---

### How it works

1. **Click** *IDA-ICE Import Results* and **select the corresponding .idm file** (created in [*IDA-ICE Export*](#ida-ice-export)).
2. The plugin iterates over all rooms defined in SIMULTAN under the Roomlist component. For each zone it searches the simulation output folder and subfolders for matching result files (e.g., ZONE-ENERGY.prn, TEMPERATURES.prn).
3. For each room, the plugin parses the relevant files: heating/cooling loads from *ZONE-ENERGY.prn*, temperatures from *TEMPERATURES.prn*. 
4. Within SIMULTAN these files get stored under the components: `IDA ICE Analyses` > `Results`. Time series are stored as both table and graph parameters.

---

```{figure} img/Import_results_comp.png
---
name: Import_results_comp
---
Csomponents filled with simulation results
```

---

> Under the *Value Fields* tab in SIMULTAN new Tables and Graphs should be added.

---

## Update Simulation Data

This function updates the simulation and *Warmup Data* in the current SIMULTAN project.
The corresponding components are located in the *ComponentBuilder* under `LivingLab` > `IDAICEAnalysis` > `Simulation Data` (see {numref}`simulationdata_components`).
When executed, these components are exported into the IDA-ICE model file, ensuring that the simulation runs over the correct time interval.

```{note}
**Warmup Phase**  
The warm-up phase is a preliminary simulation period during which the building model adapts to boundary conditions and reaches a steady periodic behaviour. This ensures realistic initial conditions for the main simulation.
```

---

```{figure} img/simulationdata_components.png
---
name: simulationdata_components
---
Update Simulation Data Components
```

###  How to use

1. **Click** on `Update Simulation Data` to open the function ({numref}`updatesimdata_ui`).
2. The UI includes 3 parameters; `Warmup Start` `Simulation Start` `Simulation End`.
3. **Enter the three parameters** in ascending order, using the following format: `yyyy-mm-dd hh:mm:ss` (e.g., `2025-10-17 15:37:00`).
4. **Confirm** with `Close`.

```{figure} img/updatesimdata_ui.png
---
name: updatesimdata_ui
---
Update Simulation Data UI
```

```{note}
The `Simulation Start` parameter represents both the **End Date** of the `Warmup Phase` and the **Start Date** of the `Simulation Phase`, as these two phases are directly linked.
``` 

---

## Convert Temperature Files

The Convert Temperature Files function processes simulation output data by converting zone temperature result files from the IDA-ICE format (`.prn`) into standard CSV files. When you select a building’s `.idm` file (must **already** have been simulated), the command automatically searches for corresponding zone result files and converts them into CSV format within each room or zone subfolder.

This conversion simplifies further data analysis and comparison with measured or processed sensor data, ensuring that all temperature datasets share a consistent and easily readable format.

> The conversion process does not alter the simulation results — it only changes the file format for improved accessibility and compatibility with other tools.