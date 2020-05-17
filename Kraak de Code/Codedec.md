---
layout: default
title: Code Decoder
nav_order: 4
has_toc: true
parent: Kraak de code
---

# Code Decoder

We hebben de remote controller behandelt, maar moeten natuurlijk ook nog de decoder voorzien. Om de code volledig te begrijpen zullen we ook een kleine schets van de verbonden pinnen maken. We zullen elke pin van de A4988 overlopen. VMOT is samen met GND verbonden met een externe bron van 8V, hiertussen staat ook nog een elco van 100uF, deze spanningsbron stuurt de motor aan. VDD en GND zijn verbonden met de 5V-pin, respectievelijk de GND-pin van de Arduino, dit zal de A4988 aansturen. De pinnen 2B, 2A, 1B, 1A zijn verbonden met de stappenmotor, zij dragen de voltage pieken over richting de stappenmotor om zo de rotatie te veroorzaken. Reset en sleep zijn aan elkaar verbonden. De steppin is verbonden aan digitale pin 2 en de dirpin aan digital pin 3 van de Arduino. MS2 en MS3 zijn aan de ground verbonden en MS1 is aan de 5V verbonden, zo zorgen we ervoor dat de stappenmotor met stappen van 0.9° vooruit zal gaan. Ook zijn er 4 switches verbonden tussen de digitale pinnen 4 tot en met 7 en de 5V-pin van de Arduino. Aan digitale pin 8 wordt de led verbonden die in serie met een weerstand van 470 Ohm richting de ground gaat.

```cpp
#include <Arduino.h>
#include <math.h>

#define stepPin 2
#define dirPin 3
#define sw1 4
#define sw2 5
#define sw3 6
#define sw4 7
#define ledPin 8
float angle = 0;
float dif = 0;
float remainder = 0;
int length = 0;
int switcher=0;

void setup() {
  Serial.begin(9600);

  pinMode(stepPin, OUTPUT);
  pinMode(dirPin, OUTPUT);
  pinMode(sw1, INPUT_PULLUP);
  pinMode(sw2, INPUT_PULLUP);
  pinMode(sw3, INPUT_PULLUP);
  pinMode(sw4, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);

  digitalWrite(dirPin, LOW);
  digitalWrite(stepPin, LOW);
  digitalWrite(ledPin, LOW);
}

void loop() {
  //Only do something if a new serial (coming from the bluetooth module) is available
  if(Serial.available()>0){
    dif = Serial.read();
    angle += round(dif/22.5)*22.5;

    //Angle interval must be between 180 & -180
    if(angle>180) angle -= 360;
    else if(angle<=-180) angle += 360; 

    //Set the right direction in which the motor will rotate (depends of the connection of the coils)
    if(dif<0){
      digitalWrite(dirPin, LOW);
    }
    else {
      digitalWrite(dirPin, HIGH);  
    }
    
    //Make the clock pulse with the right length
    length = 50*round(dif/22.5);
    //Move the motor
    for (int i = 0; i < length; i++){
      digitalWrite(stepPin, !digitalRead(stepPin));
      delayMicroseconds(500);
    }
  }
  //Check if led must be turned on in this setting
  switcher = angle/22.5;
    switch(switcher){
      case 0:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 1:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 2:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 3:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 4:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 5:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 6:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 7:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 8:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -1:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -2:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -3:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -4:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -5:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -6:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -7:
        if(digitalRead(sw1)==0&&digitalRead(sw2)==0&&digitalRead(sw3)==0&&digitalRead(sw4==0)) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      default:
        digitalWrite(ledPin, HIGH); 
        Serial.write("De hoek is geen veelvoud van 22.5");
    }
}
```