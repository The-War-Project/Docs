---
layout: default
title: Realisatie
nav_order: 4
has_toc: true
parent: Veldslag
---

# Realisatie

![Prototype1](../Images/RFIDArduinoBoard.png)

In bovenstaande figuur is een eerste prototype weergegeven. Hier werd gebruik gemaakt van een breadboard om de MISO, MOSI en SCK pinnen te verdelen over al de sensoren.  De sensoren staan op een redelijke afstand van elkaar zodat ze elkaar niet beïnvloeden. Door gebrek aan houten platen zijn de sensoren in latten vergrendelt samen met de ID tags. Hieronder zijn twee filmpjes terug te vinden van dit prototype. Op een filmpje worden de ID tags op de sensoren geplaatst waardoor in het andere filmpje te zien is dat telkens er een nieuwe tag bij komt, de sensor zijn ID weergeeft in de monitor. Als alle ID tags op hun plaats staan is het slot ontgrendeld. 

![gif filmpje](../ImagesArne/film.gif)

![gif filmpje](../ImagesArne/monitor.gif)

De zelf gemaakte PCB wordt dan opgestart door eerst een bootloader er op te branden waarna later, via een Arduino Uno, de code kan geüploaded worden.