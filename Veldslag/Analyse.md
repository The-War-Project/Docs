---
layout: default
title: Analyse
nav_order: 1
has_toc: true
parent: Veldslag
---

# Analyse

## Technologieën

Om de pionnen te detecteren is er nood aan een sensor. Tijdens het opzoeken van technologieën kwamen we uit op twee verschillende mogelijkheden. We zouden gebruik kunnen maken van het hall effect of gebruik van RFID modules. Hieronder zullen beiden vergelijkt en onderzocht worden om zo tot een keuze te komen voor de veldslag puzzel.

### Hall effect

Een eerste mogelijkheid is het gebruik van hall effect sensoren. Wanneer er geen extern magnetisch veld in de buurt van de sensor gebracht wordt, zal de output spanning gelijk zijn aan nul. Indien er toch een extern magnetisch veld in de buurt van de sensor komt zal er meer stroom geleiden wat tot een grotere output spanning zal leiden. 

Om deze technologie te implementeren zouden we gebruik moeten maken van magnetische staven, elk met een verschillende magnetische sterkte. Dit brengt echter enkele problemen met zich mee. 

* Het bestellen van op maat gemaakte magnetische staven zou ten eerste al duur alsook moeilijk te verkrijgen zijn.

* Staven kunnen elkaar beïnvloeden zodat de gemeten magnetische veldsterkte niet overeenkomt met de verwachte waarde. Andere toestellen kunnen ook een magnetisch veld creëren dat groot genoeg is om de resultaten te beïnvloeden.

* Het ontwerp voor de pinnen zal moeilijker zijn. De magnetische staven moeten echter redelijk lang zijn. Het verstoppen van de puzzel zal ook moeilijker worden aangezien er gaten in het spelbord gemaakt moeten worden.

Dit is dus niet geschikt voor een puzzel waar correctheid en verstoppen belangrijk zijn. De RFID technologie voldoet hier wel aan.

### RFID

Radio Frequency Identification (RFID) is het draadloos gebruik van radio frequenties om data te transfereren. 

Uit wat bestaat zo'n systeem dan?

* RFID reader

* RFID tag

* Antenne

Alseerst hebben we een RFID tag nodig. Deze tags bestaan uit een geïntegreerd circuit alsook een antenne om de informatie die ze opgeslagen hebben over te brengen via radio frequenties. De tags kunnen dan ook passief als actief zijn. Actieve tags hebben een voeding waarmee ze opgestart worden maar wij hebben daar geen nood aan. De passieve tags zullen actief worden door een RFID reader dat een signaal stuurt naar de tag zijn antenne. De antenne absorbeerd de energie en zal hierdoor informatie over de tag terug sturen via de antenne. Passive tags zijn ook goedkoper dan actieve tags waardoor ze beter geschikt zijn voor een low cost puzzel.

Naast de tags zijn er natuurlijk ook readers nodig. Zij zullen de informatie van de tags opvragen en lezen. Indien de ID tags (pionnen) overeen komen de juiste readers zal het slot open gaan. Meer informatie hierover is [hier](./Code.html) terug te vinden.

### Conclusie

RFID is in ons geval beter wegens het precies identificeren van de pionnen. Het contactloos lezen van de ID tags staat ons ook toe om de sensoren te verbergen en de oplossing voor de puzzel niet onder de spelers hun neus te leggen. Verder is de lage kost van deze sensoren iets waar we rekening mee houden. 

## RFID Sensor

### PN532 NFC module

![PN532 Image](../Images/PN532.png)

De PN532 sensoren zijn uitermate belangrijk voor de werking van de puzzel. Ze kunnen de IDs van Mifare cards of stikkers lezen binnen een bereik van 5 tot 7 cm. De sensoren hebben ook regelbare interfaces zodat we kunnen kiezen tussen SPI, I2C of HSU. Enkele kenmerken van de sensoren volgen in onderstaande tabel.

| Parameter                 | Value               |
| :---:                     | :---:               |
| On board level shifter    | Present             |
| Interchangable interfaces | ISP, I2C and HSU    |
| Arduino compatible        | Yes                 |
| Reading distance          | 5-7 cm              |
| Supported cards           | Mifare 1K, 4k, etc. |
| Built in antenna          | On board            |

In het geval van de veldslag puzzel hebben we gekozen voor een SPI interface. Indien we met een I2C interface zouden werken, moeten we in staat zijn om het ID van de sensor aan te passen. Dit is echter niet mogelijk waardoor er dus voor SPI geopteerd wordt. Het nadeel hiervan is dat er voor elke sensor een pin toegewijd moet worden. Meer hierover in het ontwerp. 

## Vereisten

Aangezien de bekabeling zeer fragile is en de sensoren zeker niet beschadigd mogen worden is het aangeraden om deze niet in contact te laten komen met de gebruiker. Verstop de puzzel dus aan de achterkant van een plaat en vijs de sensoren op de plaat zodat de ID tags nog binnen de 5-7 cm operatie radius komen.