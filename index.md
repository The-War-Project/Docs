---
layout: default
title: Inleiding
nav_order: 1
has_toc: true
has_children: true
---
# Inleiding

## Situering

Dit project werd gemaakt als bachelor project voor het derde jaar industrieel ingenieur Elektronica & ICT aan de Technologiecampus Gent van KU Leuven. Jaar naar jaar werd er van de studenten verwacht om een auto op een parkour te laten rijden aan de hand van sensoren. Dit jaar is het echter anders. In plaats van het gebruikelijke thema is er nu gekozen voor het thema "escape room". Om een beetje in de juiste sfeer te komen hebben we in de projectweek (eerste week van het semester) een escape room bezocht en met de eigenaar gepraat over de basics van het ontwerpen van escape rooms. We hadden al snel door dat we niet enkel de elektronica zouden moeten ontwerpen, maar ook de samenhang van puzzels en de inkleding hiervan in 1 specifiek thema. Hierdoor genoten we natuurlijk een grotere vrijheid in het kiezen van de te ontwerpen puzzels. De keerzijde van de medaille was dat onze creativiteit zeer sterk op de proef werd gesteld in iets waar we geen ervaring mee hadden. Ook merkten we snel dat het niet vanzelfsprekend is om in elke puzzel complexere elektronica verwerkt te krijgen.

## Doelstellingen

Een aantal doelstellingen die we will bereiken tijdens het uitvoeren van het project zijn als volgt weergegeven:

* C++ code opstellen voor complexere arduino toestellen

* Opzoeken van datasheets en vergelijkingen kunnen maken tussen verschillende sensoren

* Een werkend PCB ontwerp maken die specifiek aan de vereisten van onze puzzels voldoen

* Leren werken met een SPI of I2C interface

* Veiligheid voor de gebruiker en bescherming voor de puzzels

## Overzicht

![RFID block diagram](../Images/rfidDiagram.png)

### Veldslag

De eerste puzzel vermeld in home zullen we vanaf nu de veldslag puzzel noemen. Een kort overzicht van de puzzel is hierboven gegeven. Een MCU, gevoed door enkele batterijen, zal sensoren aanspreken. De spelers zullen aan de hand van vorige puzzels pionnen en instructies krijgen. Aan de hand van die instructies kan men te weten komen op welke plaatse ze de pionnen moeten plaatsen. Die pionnen moeten uiteraard op de juiste sensor geplaatst worden zodat het slot ontgrendeld kan worden. 

Wat voor een technologie hebben we nodig om deze pionnen te detecteren? In de analyse gaan we na welke technologieën er bestaan om zo'n puzzel te maken. We sluiten af met een conclusie rond de gekozen technologie.

Na de keuze van de gepaste technologie is het mogelijk om een PCB te ontwerpen. Hier wordt stap voor stap opgebouwd door te beginnen met de schemas om uiteindelijk te eindigen bij het routen zelf. De code zal verder ook besproken worden.

In het hoofdstuk realistatie zullen we de werking van de puzzels in een escape room bekijken.

Tot slot sluiten we af met de belangrijkste conclusies en een evaluatie over het project. 

### Oncijfering