(Getting_started_with_the_LivingLab_Plugin)=
<!-- Kapitel vorzeitig Fertiggestellt, inhaltlich von meiner Seite lesabr, logisch und richtig-->
# Getting started with the LivingLab Plugin

## Installing the SIMULTAN-Editor
To use the plugin you need to install the latest version of the SIMULTAN Editor. The SIMULTAN Editor allows you to interact with the SIMULTAN data model through a user interface. A comprehensive user guide on how to install and use the SIMULTAN Editor can be found [here](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki).

## Installing the LivingLab Plugin
Follow the step-by-step instructions below to install the LivingLab Plugin correctly:

1. Start your **SIMULTAN** application
2. Open the **General** tab
3. In the **General** tab, go to the **Options** area. Click on the `Plugins & Updates` button (puzzle piece icon) to open the feature (see {numref}`download_instructions`).

```{figure} img/download_anleitung.png
---
name: download_instructions
---
Plugins & Updates button in the General tab
```

4. The window that opens should look like this {numref}`Plugin-Updates_UI`

```{figure} img/Plugin-Updates_UI.png
---
name: Plugin-Updates_UI
---
Plugins & Updates window to install Plugins
```

5. Under the **Add** option, you can add any existing plugin by providing its `Plugin-Name`. This makes it straightforward to integrate new plugins (see {numref}`Plugin_add`).  
**LivingLab-Plugin-Name:** `LivingLabPlugin`

```{figure} img/Plugin_add.png
---
name: Plugin_add
---
Adding Plugins using the Plugin-Name
```

6. Press the **Install** button. Once the installation is complete, SIMULTAN will ask you to restart the application. After restarting, a new tab called **LivingLab** will appear.


## Running the Example
To verify that everything was installed correctly, open [install_test_model.simultan](files/install_test_model.simultan) in your SIMULTAN Editor (username and password: `admin`). Follow the instructions in the chapter *Running a Simulation*. <!-- Nur falls dieses Kapitel befüllt wird--> <!-- Anderes test_model einfügen, vllt ganzen ZIP ordner damit .config datei dabei ist!-->

---

If this works fine and you are getting plausible results the installation was successful.

