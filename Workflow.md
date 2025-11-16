(Workflow)=

# Workflow

This chapter describes the **Plugin’s Functions** and explains how to use them. The SIMULTAN *LivingLab Plugin* provides a broad set of features and a tailored user interface. Each feature is exposed via a dedicated button which maximises flexibility. This allows us to give users complete freedom and offer maximum functionality without compromising user-friendliness.

---

```{warning}
In the next revision of the plugin, the `Download Model` button is no longer needed.
``` 

---

## Run Workflow 

The **Workflow** button is the core of the *LivingLab Plugin*. It combines nearly all plugin tools into a single, automated sequence from data retrieval to running an IDA-ICE simulation.

After opening the Workflow UI you should see the following screen {numref}`RunWorkflwo_UI`:

```{figure} img/RunWorkflow_UI.png
---
name: RunWorkflwo_UI
---
UI for Running a Workflow in the *LivingLab Plugin*
```

---

### Config File Path

 The `config` file (configuration file) contains settings that control the plugin behaviour. For this plugin the file typically includes the API username, API password, the sensor endpoint (or sensor mapping), and other parameters required by the workflow. The `config` file has to be stored in the **same folder** as the corresponding SIMULTAN file.


```{Tip}
If you cannot find your SIMULTAN file folder on Windows, enable "Hidden Objects" in File Explorer.
```

---

### Execution Mode

The Workflow supports two execution modes:
- **Continuous:**  
  - `Number of Runs` specifies how many times the simulation should repeat.   
  - The **interval** for repeated runs is defined in the `config` file > ...<!-- Information von Zsombor wo Intervall im config File definiert wurde-->   
**Tip:** Setting `Number of Runs = -1` triggers continuous, indefinite repetition.
- **Specific Range:**   
  - Define a concrete time window by filling the `Simulation Start` and `Simulation End` fields; the workflow runs only for this period.
<!-- ⚠️ Vorschlag: Dokumentieren Sie genau, welcher .config-Schlüssel das Intervall definiert (Name, Einheiten), und geben Sie eine Parameterbeschreibung an (z. B. Millisekunden, Sekunden, Minuten). -->

---

### Running the Workflow

**Starting the Simulation:**   
Given the configured `Execution Mode`, the plugin retrieves the corresponding weather and sensor data from the API.

**Simulationphase:**  
The model is exported automatically to IDA-ICE. Instead of synthetic or standard boundary conditions, the workflow substitutes the measured weather and sensor data downloaded from the API as the boundary for the IDA-ICE simulation. Data required for clean exports are organised in SIMULTAN components and annotated with taxonomies so that IDA-ICE can uniquely identify them. Finally, the IDA-ICE simulation is started automatically.

**Results:**  
Because the simulation uses measured input data, results from the workflow are typically more representative of real operation than standard simulations. Using the LivingLab UI, a full end-to-end run can be completed quickly.
