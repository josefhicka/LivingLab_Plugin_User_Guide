(Introduction)=

# Introduction

Notizen:

Wichtigster TEil des Living Lab Plugin ist das Herunterladen der Sensor-Daten (live) aus dem Labor in der FH Burgenland.

## Taxonmien

1:09:00 Das Living Lab Plugin kommt auch mit eigenen Taxonomien. Wichtig sind die Sensoren, es gibt unterschiedliche Sensoren Arten. Mit den richtigen Komponenten kann man die DAten als graph abbilden! Daten können durch das drücken des richtigen Knopfes auf das aktuellste automatisch AKtualisiert werden. 

## Buttons des Plugins

### Download Model Button

veraltet, wird in naher zukunft entfernt

### Workflow Button

1:11:00 braucht unbedingt ein .config file. Findet man immer in den Ordnern der Simultan-Dateien (versteckte Ordner). Informationen des .config files: Benutzername für die API, Passwort, DAten IDs, ... weitere Infos

Run Workflow fenster: 
1. config File wie oben beschrieben
2. Excution Mode: 1:12:00
    - specific Range definiert dauer der Simulation in IDA-ICe über die Felder Simulation Start: und Simulation End:
    - Continuous: Simulation wird regelmäßig rückblickend gemacht. Im config File kann man das Intervall definieren, Andreas / Zsombor fragen wo genau das hinterleft ist. (-1 steht für unendlich) 
3. Number of Runs gibt an wie oft die Simulation wiederholft wird.

Interner Ablauf wenn workflow gestartet wird: Plugin holt sich die WEtterdaten für den Zeitraum, die Sensordaten für den Zeitraum, IDA-ICE-Plugin wird im hintergrund gestartet --> exportiert das Modell. Nimmt anstatt von Standard werten die heruntergeladenen echt WEtterdaten welche in den Simultans Componenten/Taxonmien hinterlegt sind und Simuliert anschließend das Modell mit den echten Daten

´´´{warning}
Abstände beim Benutzernamen verursachen Probleme, Programm kann nicht erfolgreich simulieren und stürzt ab!
´´´ 