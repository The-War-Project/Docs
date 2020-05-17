---
layout: default
title: Ontwerp
nav_order: 2
has_toc: true
parent: Kraak de code
---

# Ontwerp

Nu we weten welke technologiëen en bijkomend welke specifieke modules we gaan gebruiken kunnen we overgaan tot het maken van het schema. We moeten wel opmerken dat het schema werd gemaakt in combinatie met het schrijven van de code. Het is namelijk niet zinvol om inputs en outputs te gaan verbinden die niet nodig zijn en het is een groter probleem wanneer inputs en outputs die verbonden moeten zijn zodat de code kan werken, niet verbonden zijn. In ons schema hebben we één input verbonden die overbodig is.

Ook zullen we enkel een schema ontwerpen voor onze remote controller. Dit doen we omdat we enkel hiervoor een PCB fysiek zullen maken.

## Schema

We hebben ons schema getekend via KiCad en hebben gebruik gemaakt van een reeds bestaand Arduino schema te vinden op deze [link](https://github.com/rheingoldheavy/arduino_uno_r3_from_scratch). Op dit schema hebben we echter bepaalde dingen weggelaten om onze PCB een zo laag mogelijk verbruik te geven. Het schema dat we zo bekomen ziet u in de volgende figuur.

![Kicad schematic](../ImagesRobin/kicadschema.png)
