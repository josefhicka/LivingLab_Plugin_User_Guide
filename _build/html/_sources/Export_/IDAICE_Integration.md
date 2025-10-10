(IDAICE_Integration)=

# IDAICE Integration

This chapter documents the three IDA-ICE related features provided by the LivingLab Plugin: **IDA-ICE Export**, **IDA-ICE Simulate**, and **IDA-ICE Import Results**. Each feature is available via its own button in the LivingLab UI and is intended to support an end-to-end workflow: export a SIMULTAN model to an IDA-ICE model file (.idm), run IDA-ICE simulations, and import the resulting time series back into SIMULTAN.

---

## IDA-ICE Export

The **IDA-ICE Export** button converts the active SIMULTAN building model into one or more IDA-ICE model files (.idm). The export converts geometry, constructions, material properties, and the ESBO plant (or a simplified plant representation) from the SIMULTAN data model into an IDA-ICE compatible format.

---

### IdaIce_Export_UI

**IDA-ICE Export dialog / Save dialog**

#### How to use

1. Click IDA-ICE Export in the LivingLab toolbar.
2. A save dialog opens — choose the output folder and file name (project_name.idm).
3. Confirm the file name and start the export. A progress indicator or log window shows the export pipeline status.
4. On completion the .idm file(s) are written to the chosen folder; any additional files required by IDA-ICE (support files, plant definitions) are placed in subfolders according to the export log.

#### Export pipeline (six steps)

The export executes a six-step pipeline. Each step includes validation and logging so you can trace issues if they occur:

1. **Project validation**  
   Checks that the loaded SIMULTAN project is consistent and that required objects (zones, constructions, plant definitions) are present. Validation warnings and errors appear in the export log.
2. **Geometry extraction & processing**  
   Extracts zones, surfaces, openings and shading elements and transforms them into IDA-ICE geometry. This step resolves zone names and mappings that will be used later to link results back to SIMULTAN.
3. **Material & construction export**  
   Exports material properties and layered constructions. Constructions are written in a form compatible with IDA-ICE material models.
4. **Plant model generation**  
   Generates the heating/cooling plant description. For complex systems, ESBO models are generated; for simpler analyses an Ideal plant representation is used. The chosen plant type is recorded in the export log.
5. **Environment & site configuration**  
   Configures site properties (location, weather references) and any boundary conditions required by IDA-ICE.
6. **File save & finalization**  
   Writes the .idm file(s) and any companion files to disk and closes the export session.

> If the export log contains validation errors, correct the underlying SIMULTAN model (missing constructions, unnamed zones, invalid taxonomies) before re-exporting.

#### Tips & common checks

- Ensure every zone has a unique name — names are used to map IDA-ICE results back to SIMULTAN.
- Verify that required constructions and material properties are assigned to surfaces.
- If you require a specific plant representation, confirm the export options or set the plant type in the .config / export preferences (see suggestions below).

---

## IDA-ICE Simulate

The **IDA-ICE Simulate** button launches IDA-ICE to run simulations using selected .idm model files. The plugin starts IDA-ICE, monitors the external process, and reports completion and basic status to the user. Typical simulation outputs are text-based result files such as TEMPERATURES.prn, ZONE-ENERGY.prn, and ENERGY.prn.

---

### IdaIce_Simulate_UI

**IDA-ICE Simulate dialog (select IDA-ICE exe path & .idm file)**

#### How to use

1. Click IDA-ICE Simulate.
2. In the dialog, specify the path to the IDA-ICE executable (e.g., C:\Program Files\IDA-ICE\bin\ida-ice.exe) if prompted. The plugin stores this path for subsequent runs.
3. Click Simulate, then select the .idm file you want to run.
4. The plugin launches IDA-ICE and polls the ida-ice process every 5 seconds to monitor progress.
5. When the process exits, the plugin reports completion and lists the result files produced.

> Make sure IDA-ICE is installed, licensed and that the selected executable path is correct. Simulations will not run if the executable cannot be launched.

#### Produced output

- TEMPERATURES.prn — room/zone operative temperatures (time series).
- ZONE-ENERGY.prn (or ENERGY.prn) — heating / cooling loads and energy results.
- Other standard IDA-ICE result files depending on simulation settings.

#### Monitoring & failure modes

- The plugin periodically polls the OS process list to detect when the ida-ice process terminates. If IDA-ICE spawns helper processes, the plugin monitors the main PID only.
- If the simulation fails to start, check: executable path, user permissions, presence of required input files, and available disk space.
- If the simulation runs but no result files are generated, inspect the IDA-ICE log files in the simulation output folder for runtime errors.

---

## IDA-ICE Import Results

The **IDA-ICE Import Results** button reads IDA-ICE simulation output files and transfers the numerical results back into the SIMULTAN data model. The import parses per-room result files and creates or updates components that contain time-series data (tables and graphs) for heating loads, cooling loads and operative temperatures.

---

### IdaIce_Import_UI

**IDA-ICE Import Results dialog (select .idm file and result folder)**

#### How it works (high level)

1. Click IDA-ICE Import Results and select the corresponding .idm file (or the simulation output folder).
2. The plugin iterates over all rooms / zones defined in the .idm / SIMULTAN mapping. For each zone it searches the simulation output folder and subfolders for matching result files (e.g., ZONE-ENERGY.prn, TEMPERATURES.prn).
3. For each room found, the plugin parses the relevant files: heating/cooling loads from ZONE-ENERGY.prn, temperatures from TEMPERATURES.prn.
4. The plugin creates or updates SIMULTAN components and assigns taxonomy tags so the imported data can be identified and exported later. Time series are stored as both table and graph parameters where applicable.

#### Expected result structure

Result files are typically stored in subfolders created per simulation run and per building/zone. The plugin expects a naming structure that allows it to locate room-specific files using zone names or IDs exported during the IDA-ICE export step.

#### Mapping & taxonomy

Successful import depends on the mapping between SIMULTAN zone identifiers and IDA-ICE room identifiers. The export step stores identifiers/taxonomies that are later used by the importer to link result files to SIMULTAN components.

If zone names were changed after export or if export used non-unique names, the importer may fail to find corresponding result files. Keep zone names stable between export, simulation and import.

#### Troubleshooting common issues

- Missing result files — verify the simulation completed successfully and that result files exist in the output folder.
- Name mismatches — ensure zone/room names are identical between SIMULTAN and IDA-ICE export. If you renamed zones after export, re-export before simulating.
- Parsing errors — check the result file format (decimal separator, header lines) and the importer log for line parsing errors. Different localisations (e.g., comma vs dot as decimal separator) can break parsers.
- Large datasets — importing long time series for many zones can be memory and time intensive. Consider importing a subset or processed (aggregated) results if performance becomes an issue.

> Keep a copy of the export `.idm` and the simulation output folder for reproducibility. This helps debugging and makes it easier to re-run imports if required.

---

## Actionable Documentation Improvements & Suggestions

- Include example .idm folder layout and example result files (small sample files for TEMPERATURES.prn and ZONE-ENERGY.prn) so users can test the importer without running full simulations.
- Add an example export log that shows the six pipeline steps and example warnings/errors, making it easier to interpret real logs.
- Document the taxonomy pattern used to tag components (exact naming convention). Provide examples: e.g. livinglab:idaice:zone:<zone_name>:temperatures.
- Specify config keys (if applicable) — for example, IDAExePath and where this is stored; also document file permission requirements.
- Provide an example of the IDA-ICE executable path for Windows/macOS/Linux and a short checklist for common simulation failures (license, disk space, path with spaces).
- Clarify localisation and parsing rules for result files (decimal separator, date format, header parsing). Add a small section describing how the importer handles different locales.
- Add a brief performance note: approximate runtime and disk usage expectations for typical model sizes (small / medium / large) and guidance on importing large result sets (batch import or subset).
- Security note: recommend storing executable paths and credentials in project .config files with restricted filesystem permissions; document secure alternatives where possible.
