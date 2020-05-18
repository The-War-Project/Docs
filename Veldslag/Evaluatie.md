---
layout: default
title: Evaluatie
nav_order: 5
has_toc: true
parent: Veldslag
---

# Evaluatie

Na heel wat testen, code schrijven en een PCB ontwerp hebben we gebruik kunnen maken van de RFID technologie. Hieruit kunnen we enkele conclusies trekken over de dingen die goed werken alsook minder goed werken.

Om te starten is de RFID technologie superieur ten opzichte van de sensoren op basis van het Hall effect. Door deze keuze is het programmeer werk heel wat verminderd en de nauwkeurigheid van de te lezen pionnen gestegen. Het nadeel van deze RFID technologie is dan dat de sensoren niet te dicht op elkaar mogen liggen zodat ze elkaar niet gaan beïnvloeden en het hele systeem vast loopt.

Door het kleine PCB ontwerp en gebruik van batterijen is het mogelijk om dit zeer goed te verstoppen voor de spelers. Ondanks de batterijen lang kunnen meegaan is de lage verbruik modus niet ingeschakeld. 

Een bijkomend nadeel van de PN532 sensor is echter dat deze niet tesamen met andere sensoren kan gebruikt worden als we een I2C interface willen gebruiken. Ze delen allemaal eenzelfde ID waardoor individuele aanspraak niet mogelijk is.

Een realisatie van de puzzel is zeker mogelijk mits er een herontwerp van de PCB mogelijk is.

## Uitbreidingen

Indien de hosts van de escape rooms meerdere sensoren willen gebruiken is er de mogelijkheid om I/O extenders te gebruiken. De Atmega328P heeft enkel 23 I/O pinnen maar met de extender kan dit aantal vele keren groter zijn.

Een interface met de gebruiker, bijvoorbeeld bluetooth, behoort ook tot de mogelijkheden. Immers, indien de puzzel nu zou vast lopen is het niet mogelijk om deze te resetten zonder de knop fysiek in te drukken.

Als laatste zouden we een low power mode kunnen implementeren om het batterijverbruik te minimaliseren.