---
layout: default
title: Evaluatie
nav_order: 5
has_toc: true
parent: Veldslag
---

# Evaluatie

Na heel wat testen, code schrijven en PCB ontwerp kunnen we tot een paar conclusies komen.

Om te starten is de RFID technologie superieur ten opzichte van de sensoren op basis van het Hall effect. Door deze keuze is het programmeer werk heel wat verminderd en de nauwkeurigheid van de te lezen pionnen gestegen. Het nadeel van deze RFID technologie is dan dat de sensoren niet te dicht op elkaar mogen liggen zodat ze elkaar niet gaan beïnvloeden en het hele systeem vast loopt.

Door het kleine PCB ontwerp en gebruik van batterijen is het mogelijk om dit zeer goed te verstoppen voor de spelers. Alhoewel de de batterijen lang kunnen meegaan is de low power consumption mode niet ingeschakeld. 

Een bijkoment nadeel van de PN532 sensor is echter dat deze niet tesamen met andere sensoren kan gebruikt worden als we een I2C interface willen gebruiken. Ze delen allemaal eenzelfde ID waardoor individuele aanspraak niet mogelijk is.

