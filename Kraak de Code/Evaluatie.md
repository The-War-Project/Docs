---
layout: default
title: Evaluatie
nav_order: 6
has_toc: false
parent: Kraak de code
---

# Evaluatie

Ten eerste hebben we onderzocht welke technologieën het best zullen werken in combinatie met de Arduino en of deze de juiste functionaliteiten kunnen verwezenlijken. Het is duidelijk dat de MPU6050, de stappenmotor en de HC-05 voor een correcte werking hebben gezorgd. We moeten natuurlijk steeds kritisch zijn en nagaan of er geen betere technologieën mogelijk waren. 

De MPU6050 geeft redelijk goede resultaten maar is misschien iets teveel van het goede. Onze resultaten hoefden niet zo extreem nauwkeurig te zijn aangezien we 22.5° per stap gebruikten. Ook hebben we hierop een accelerometer die we niet gebruikt hebben. Indien we low-power willen gaan, zouden we deze module ook kunnen herschetsen om de overhead weg te werken.

De bluetooth-modules doen wat hun gevraagd wordt en sturen de data onmiddellijk naar elkaar door. Hierdoor is de delay zeer laag. Men kan natuurlijk voor andere communicatiemiddelen kiezen, maar door de dedicated verbinding tussen 2 modules en het onnodig zijn om aan de informatie te geraken via een 3de partij is bluetooth de gekozen technologie.

De A4988 en zijn stappenmotor zijn ook goed gekozen aangezien het compact en goed afstelbaar is. De meeste motoren die men elektrisch aanstuurt, steunen op het principe van elektromagnetisme waardoor het onnodig is om nog verder te gaan zoeken naar andere motoren. 

Nadat we deze modules gekoppeld hebben aan de Arduino hebben we het PCB ontworpen dat er op het eerste zicht goed uitzag. Jammer genoeg konden we na het solderen de bootloader hier niet op branden waardoor we genoodzaakt waren onze PCB te laten vallen voor wat het was om toch maar de correcte werking aan te kunnen tonen via een Arduino.

De code lijkt op het eerste zicht ook goed maar zoals met elke code kan er meestal wel iets beter geschreven worden. Dit merken we ook aan het feit dat er een zeer grote vertraging optreedt indien we de schakelaars zullen verbinden aan de schakeling. De code is duidelijk niet efficiënt genoeg geschreven en de volledige puzzel kan dus niet vlot genoeg werken.

## Uitbreidingen

Men kan de stappenmotor tot 0.1125°/stap laten gaan waardoor we stappen van 2.8125 graden zouden kunnen zetten. Dit komt overeen met 128 verschillende symbolen waardoor het kraken van de code zeer tijdrovend wordt. Hiervoor zijn dan ook 7 schakelaars nodig. De complexiteit van de puzzel kan dus steeds verhoogd of verlaagd worden.

We kunnen zoals hiervoor vermeldt de puzzel sterk verbeteren door de code efficiënter te schrijven waardoor er geen vertragingen zullen optreden. 

Als laatste uitbreiding kunnen we een resetbutton implementeren die ervoor zorgt dat de stappenmotor steeds een vaste beginpositie heeft en dit niet handmatig verdraaid moet worden. Via een eindeloopschakelaar kan men hem dan laten draaien tot men op de juiste positie komt. Hierna zal het draaien stoppen en kan het spelletje beginnen.