(Simultan_Basics)=

# Simultan Basics

As with all other SIMULTAN plugins, the LivingLab-Plugin offers a large number of new tools and possibilities. However, there are basic building blocks that are relevant in every plugin and that you therefore need to understand.

The SIMULTAN data structure consists of two main elements:

1. [Taxonomies](#taxonomies)
2. [Components](#components)

---

## Taxonomies

Taxonomies are **classification systems** used to organize elements into **hierarchical categories and subcategories**. They help structure complex models and define relationships between entities. Taxonomies also define the storage locations of data. When new data enters the data model through simulations or queries, it can be stored under the correct taxonomy using algorithms.

---

```{note}
Components that are not assigned to a taxonomy are completely ignored by the plugin.
``` 

---

### LivingLab Relevant Taxonomies

In {numref}`livinglabtax`, you can see all the new taxonomies which come with the plugin. These are designed for sensors and weather data in accordance with the plugin.

```{figure} img/LivingLabTax.png
---
name: livinglabtax
---
Overview of LivingLab taxonomies
```

This system ensures accurate data exchange. This enables the subsequent generation of a fully automated workflow. More on this in the chapter [Run Worklow](Workflow.md#run-workflow).
We recommend starting with the attached [file](files/install_test_model.simultan) to learn how to use the plugin. It also ensures synchronization and reduces the chance of errors.

---

## Components
The *ComponentBuilder* represent the functional building blocks of a simulation model as shown in {numref}`components_beispiel`. Examples include heat pumps, fans, results fields and much more. Each component has specific **properties** and **parameters** relevant for simulation.

```{figure} img/components_beispiel.png
---
name: components_beispiel
---
Some components of a data model

```

---

### Intersection of Taxonomies and Components

Each component in the Plugin should be linked to a taxonomy. This is the case if a taxonomy name is linked in the `List` column. However, if this field **remains empty**, it means that this component is **inactive** and is ignored by the data model.

Furthermore, it is essential to note that not only the taxonomies themselves but also the overall data structure and availability of corresponding components are critical for correct system behavior. For example, measurement data cannot be downloaded or processed if no corresponding components exist for these data types. Missing or inactive components therefore directly affect which data will be retrieved and integrated into the model, highlighting the importance of a complete and well-maintained component definition.