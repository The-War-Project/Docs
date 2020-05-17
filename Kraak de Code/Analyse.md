---
layout: default
title: Analyse
nav_order: 1
has_toc: true
parent: Kraak de code
---

# Analyse

Om te beginnen bekijken we deze puzzel wat meer in detail. We zullen 2 modules nodig hebben om deze puzzel te verwezenlijken, de afstandsbediening (remote controller) enerzijds en de decoder anderzijds. De remote controller moet de draaiing rond zijn eigen as kunnen meten. Hiervoor zullen we dus een bepaalde technologie moeten gebruiken. Deze draaiing moet verwerkt en doorgestuurd worden naar de decoder die deze informatie nog eens zal verwerken om de schijf op de juiste positie te zetten. Hierna moet er nog gekeken worden of deze positie klopt met de stand van de schakelaars. Dit is dus ook een werkje voor de decoder. De communicatie tussen beide delen zal ook via een bepaalde technologie moeten gebeuren evenals het draaien van de schijf. Aangezien we steeds met Arduino's zullen werken moeten we dus modules vinden die gemakkelijk te gebruiken zijn in combinatie met Arduino.

## De sensor (draaiing rond eigen as)

### Coriolis Effect

Voor de sensor kunnen we beroep doen op het Coriolis effect. Dit effect bestaat door combinatie van een rechtlijnige beweging over een draaiend oppervlak. Hierbij is het de bedoeling dat de rechtlijnige beweging niet in de richting van de draaiing is, anders krijgt men gewoon een sterkere draaiing. Indien men ervoor zorgt dat deze rechtlijnige beweging rechtlijnig blijft vanuit een stilstaand perspectief, dan zal er een bepaald pad bestaan op het draaiend oppervlak. Dit pad zal niet rechtlijnig zijn doordat die oppervlak ronddraait. Door toepassen van enkele formules kan men hieruit de verdraaiing van dit oppervlak halen gedurende de periode waarin de rechtlijnige beweging gemaakt werd. Zo krijgt men een bepaalde hoeksnelheid waarmee het oppervlak draait.

### MPU-6050

De MPU-6050 is een module die hoekverdraaiingen kan meten (gyrometer) steunend op het Coriolis effect. Deze hoekverdraaiingen kunnen gemeten worden rond de x-, y- en z-as. Ook heeft deze module een accelerometer om de versnelling over deze assen te meten. In onze toepassing zijn we echter enkel geïnteresseerd in de gyrometer. De module bevat ook een digital motion processor die de data die binnenkomt zou kunnen verwerken, hierdoor zal onze Arduino minder belast worden. We hebben van de DMP geen gebruik gemaakt omdat het rekenwerk dat de Arduino moet verrichten al aan de lage kant was. Enkele specificaties kunt u hieronder zien.

| Parameter                   | Value               |
| :---:                       | :---:               |
| Input Voltage (VDD)         | 2.375V - 3.46V      |
| Logic voltage (VLOGIC)      | 1.7V - VDD          |
| Arduino compatible          | Yes                 |
| Supported Interface         | I2C                 |
| Analog-to-Digital Converter | 16 bit              |
| Range (Gyrometer)           | 250°/s - 2000°/s    |

## Communicatie tussen Arduino's

Voor de communicatie kunnen we gebruiken maken van een WiFi-module of een Bluetooth-module. Een WiFi-module lijkt ons een beetje teveel van het goede aangezien ze enkel naar elkaar informatie moeten doorsturen en de informatie dus niet voor iedereen bereikbaar hoeft te zijn. Daarom zullen we gebruik maken van 
Bluetooth. 

### Bluetooth

Het principe van Bluetooth steunt op hetzelfde principe als de radio maar werkt in de 2.4GHz-band. Ook is het zendvermogen niet zo sterk als een radioverbinding waardoor men maar enkele meters (~10m) ver kan zenden. Men kan natuurlijk het zendvermogen gaan opdrijven om een groter bereik te krijgen maar dit is onnodig voor onze toepassing.

### HC-05

De HC-05 is een Bluetooth module waarbij men op voorhand kan instellen waarmee verbinding gemaakt wordt. De module kan de datamode of de AT command mode aannemen. In de AT command mode, kan men kiezen of de module zich gedraagt als een slave of als een master. Indien het een slave is, zal er verbinding gemaakt worden met elk apparaat dat een verzoek stuurt om te verbinden. Indien het een master is, zal de module expliciet gaan zoeken naar een specifiek adres om verbinding mee te maken. Indien dit apparaat niet in de range is, zal de master wachten tot hij het vindt en geen verbinding maken met apparaten die hem een verzoek sturen om te verbinden. We moeten dus zorgen dat onze Bluetooth-modules met elkaar verbinding zullen maken. In de datamode zal de binnenkomende data doorgestuurd worden naar de verbonden module en andersom. Enkele specificaties zijn hieronder opgelijst.

| Parameter                   | Value            |
| :---:                       | :---:            |
| Input Voltage (VDD)         | 3.2V - 6V        |
| Logic voltage (VLOGIC)      | 3.2V - VDD       |
| Arduino compatible          | Yes              |
| Supported Interface         | UART             |
| Protocol                    | IEEE 802.15.1    |
| Range                       | ~10m             |
| Supported baud rates        | 9600 - 460800    |