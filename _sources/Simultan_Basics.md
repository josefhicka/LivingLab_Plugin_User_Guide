(Simultan_Basics)=

# Simultan Basics

As with all other Simultan plugins, the LivingLab plugin offers a large number of new tools and possibilities. However, there are basic building blocks that are relevant in every plugin and that you therefore need to understand.

The SIMULTAN data structure consists of two main elements:

1. [Taxonomies](#taxonomies)
2. [Components](#components)

---

## Taxonomies

Taxonomies are classification systems used to organize elements into hierarchical categories and subcategories. They help structure complex models and define relationships between entities.  
Taxonomies also define the storage locations of data. When new data enters the data model through simulations or queries, it can be stored under the correct taxonomy using algorithms.

```{note}
**Components that are not assigned to a taxonomy are completely ignored by the plugin.**
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

This system ensures accurate data exchange. This enables the subsequent generation of a fully automated workflow. More on this in chapter [Run Workflow](Plugin_Features.md#run-workflow).
We recommend starting with the attached [file](files/install_test_model.simultan) to learn how to use the plugin. It also ensures synchronization and reduces the chance of errors.

---

## Components
The *ComponentBuilder* represent the functional building blocks of a simulation model as shown in {numref}`components_beispiel`. Examples include heat pumps, fans. Each component has specific properties and parameters relevant to simulation, such as power consumption.

```{figure} img/components_beispiel.png
---
name: components_beispiel
---
Some components of a data model

```

---

### Intersection of Taxonomies and Components

Each component in the data model should be linked to a taxonomy. This is the case if a taxonomy name is linked in the `List` column. However, if this field remains empty, it means that this component is inactive and is ignored by the data model.