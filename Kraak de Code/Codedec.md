---
layout: default
title: Code Decoder
nav_order: 4
has_toc: true
parent: Kraak de code
---

# Code Decoder

We hebben de remote controller behandelt, maar moeten natuurlijk ook nog de decoder voorzien. Om de code volledig te begrijpen zullen we ook een kleine schets van de verbonden pinnen maken. We zullen elke pin van de A4988 overlopen. VMOT is samen met GND verbonden met een externe bron van 8V, hiertussen staat ook nog een elco van 100uF, deze spanningsbron stuurt de motor aan. VDD en GND zijn verbonden met de 5V-pin, respectievelijk de GND-pin van de Arduino, dit zal de A4988 aansturen. De pinnen 2B, 2A, 1B, 1A zijn verbonden met de stappenmotor, zij dragen de voltage pieken over richting de stappenmotor om zo de rotatie te veroorzaken. Reset en sleep zijn aan elkaar verbonden. De steppin is verbonden aan digitale pin 2 en de dirpin aan digital pin 3 van de Arduino. MS2 en MS3 zijn aan de ground verbonden en MS1 is aan de 5V verbonden, zo zorgen we ervoor dat de stappenmotor met stappen van 0.9° vooruit zal gaan. Ook zijn er 4 switches verbonden tussen de digitale pinnen 4 tot en met 7 en de 5V-pin van de Arduino. Aan digitale pin 8 wordt de led verbonden die in serie met een weerstand van 470 Ohm richting de ground gaat.

We merken ook op dat de sleutel om de code te ontcijferen hier nog niet in geïmplementeerd is. Het lampje zal branden als alle switches open zijn. De implementatie van de ontcijfercode is slechts een kleine verandering en kan dus makkelijk veranderd worden.

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
int sw_state[4] = {0}, new_sw_state[4] = {0};
double angle = 0;
int dif = 0;
int length = 0;
int switcher=0;
bool updateLed = false;

void setup() {
  // put your setup code here, to run once:
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

  //Set state of the switches
  for (int i=0; i<4; i++){
    if(digitalRead(sw1+i)==HIGH) sw_state[i]=1;
    else sw_state[i]=0;
  }
}

void loop() {
  //Set state of switches & update every loop to see if they have changed
  for (int i=0; i<4; i++){
    if(digitalRead(sw1+i)==HIGH) new_sw_state[i]=1;
    else new_sw_state[i]=0;
  }
  //Look if switches are changed (if changed, update the led)
  if (new_sw_state[0] != sw_state[0] && new_sw_state[1] != sw_state[1] && new_sw_state[2] != sw_state[2] && new_sw_state[3] != sw_state[3]) {
    updateLed = true;
    for (int i = 0; i<4; i++){
      sw_state[i] = new_sw_state[i];
    }
  }

  //Look if new serial is coming from the bluetooth module
  if(Serial.available()>0 && !updateLed){
    dif = Serial.parseFloat();
    if (dif > 180) dif -= 360;         //Added 360 at the master side before the value was sent, so remove 360 at the slave side 
    updateLed = true;                  //After this if-statement the led will be updated because it has to be updated everytime an input changes
    angle += round(dif/22.5)*22.5;     //Get the multiple of 22.5 for the angle
  
    //Angle interval must be between 180 & -180
    while (angle>180) angle -= 360;
    while (angle<=-180) angle += 360; 

    //Set the right direction in which the motor will rotate (depends on the connection of the coils)
    if(dif<0){
      digitalWrite(dirPin, LOW);
    }
    else {
      digitalWrite(dirPin, HIGH);  
    }
  
    //Make the clock pulse with the right length
    length = 50*round(abs(dif)/22.5);
    //Move the motor
    for (int i = 0; i < length; i++){
      digitalWrite(stepPin, !digitalRead(stepPin));
      delayMicroseconds(500);
    }
  }

  //Check if led must be turned on in this setting
  if(updateLed){
    switcher = round(angle/22.5);
    switch(switcher){
      case 0:
       if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);  
        else digitalWrite(ledPin, LOW);
        break;
      case 1:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 2:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 3:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 4:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 5:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 6:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 7:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case 8:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -1:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -2:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -3:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -4:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -5:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -6:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      case -7:
        if(sw_state[0] == 0 && sw_state[1] == 0 && sw_state[2] == 0 && sw_state[3] == 0) digitalWrite(ledPin,HIGH);
        else digitalWrite(ledPin, LOW);
        break;
      default:
        digitalWrite(ledPin, HIGH); 
        Serial.write("De hoek is geen veelvoud van 22.5");
    }
    updateLed = false;
  }
}
```