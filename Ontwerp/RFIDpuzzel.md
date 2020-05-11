---
layout: default
title: RFID Puzzel
nav_order: 1
has_toc: true
parent: Ontwerp
---

# Ontwerp

## Code

De code voor de RFID puzzel is [hier](../Code/RFIDcode.md) te vinden. Bovenaan de code vinden we enkele includes terug die de juiste libraries zullen inladen die we zullen gebruiken. Vervolgens vinden we enkele declaraties van constanten en pinnen terug. Een boolean *isLocked* zal false worden zodra de juiste combinatie van RFID tags en sensoren gevonden is. Als laatste maken we drie arrays aan. Één die de pinnen van de sensoren bijhoudt, één die de ID tags van de toegelaten ID tags bijhoudt en eentje die de sensoren van de puzzel in een array bijhoudt.

Het tweede gedeelte van de code bestaat uit de setup. Hier wordt alles geïnitialiseerd. We starten met het connecteren van de seriële monitor en printen hierop een tekstje uit. Vanaf dan zal voor het aantal readers, in ons geval 8, telkens gecontrolleerd worden of deze werken. Indien ze werken zullen hun naam en firmware version in de seriële monitor verschijnen. 

Na declaraties en initialisaties komen we uit op de kern van het programma. Bovenaan de loop vinden we voorwaarde *isLocked* terug die hierboven vermeld en uitgelegd is. 
