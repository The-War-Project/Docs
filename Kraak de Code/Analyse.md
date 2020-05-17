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

Voor de sensor kunnen we beroep doen op het Coriolis effect. 