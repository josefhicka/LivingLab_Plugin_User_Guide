(Time_Handling)=

# Time Handling

Proper time management is essential when working with sensor and simulation data. This chapter explains the conversion between `DateTime` and `HourlyIndex` formats, ensuring that time representations are consistent and compatible with both human-readable and simulation-oriented workflows.

---

## Time Format Conversion

`DateTime` and `HourlyIndex` formats are two common ways to represent time in datasets and simulations. `DateTime` includes full date and time information, making it easy to trace, compare, and interpret exact moments or periods. An `HourlyIndex`, on the other hand, simply counts each hourly interval from a defined starting point—this is useful for simulations and calculations that focus on time steps rather than specific dates.

Converting between these formats is important: it lets users switch easily between human-readable times and efficient index-based processing. The ability to convert ensures flexibility when working with data, helping match the needs of both calculations and presentation.

---

```{warning}
Check that all data records in your `Csv` file are formatted consistently. Just one outlier is enough to prevent a successful conversion.
``` 

### How to use

1. Press one of the two buttons, `Convert DateTime to Hourly Indexed` or `Convert Hourly Indexed to DateTime`, depending on what you want to do.
2. Specify the year of your data. <!-- WAs ist wenn die daten in mehreren jahren sind?-->
3. Press `Browse...` to select the file you want to convert.
4. Click `Convert` to start the process.

---

```{tip}
- {numref}`Index_Converter` Both functions/UI work exactly the same way, just make sure you use the right method based on your input data.   
- Conversion also works for files with **multiple Simulation Years**. Entries from the specified year (e.g., 2025) onward get positive hourly indices; earlier entries receive negative indices.
```

---

```{figure} img/Index_Converter.png
---
name: Index_Converter
---
UI for converting time indices
```

---

*Once your time representations are aligned and consistent, you can process the data for analysis and comparison. Data Processing shows how to clean, average, and merge datasets for accurate validation.*