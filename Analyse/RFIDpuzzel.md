---
layout: default
title: RFID puzzel
nav_order: 1
has_toc: true
parent: Analyse
has_children: true
---

# RFID Puzzel

## Functionaliteit

Het doel van de puzzel is om de juiste combinaties van ID tags en sensoren te vinden. Om dit tot een goed eind te brengen hebben we nood aan 8 RFID sensoren, een LDO en een atmega328P.

### Onderdelen

Om deze puzzel tot een goed eind te brengen hebben we nood aan enkele onderdelen. Hun belangrijkste kenmerken zullen hieronder beschreven worden.

#### Atmega 328P

![Atmega Image](../Images/atmegaimage.png)

De atmega 328P is het hart van onze puzzel. Deze processor, gebruikt in arduino UNO, is gekozen omwille van het wijdverspreid gebruik en de familiariteit in eerdere jaren van onze studie. Enkele gegevens zijn weergegeven in de tabel hieronder. Belanrijk om te noteren is dat er meer dan genoeg flash memory aanwezig is voor onze kleine programmas alsook de operating frequency hoog genoeg ligt zodat we een kristal van 16MHz kunnen gebruiken voor onze toepassing.

| Parameter                      | Value            |
|              :---:             |       :---:      |
| Microcontroller                | 8-bit AVR        |
| Flash memory                   | 32 KB            |
| EEPROM                         | 1 KB             |
| SRAM                           | 2 KB             |
| I/O pins                       | 23               | 
| Interface                      | Master/Slave SPI |
| Maximum operating frequency    | 20 MHz           |