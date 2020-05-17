---
layout: default
title: Code Remote Controller
nav_order: 3
has_toc: true
parent: Kraak de code
---


# Code Remote Controller

De code die we gebruikt hebben voor de remote controller staat op deze pagina opgelijst. We hebben hiervoor gebruik gemaakt van een circ-buffer gevonden op de [link](https://github.com/dramco-edu/die-shield/tree/master/src). Hier hebben we enkele dingen aangepast om de gemiddelde waarde te krijgen van de items in de buffer.

```cpp
#include <Arduino.h>
#include "circ-buffer.h"
#include "Wire.h"

#define batteryPin A0
#define batteryLed 5
const int MPU = 0x68;                        //Address of the MPU
float elapsedTime, time, timePrev;           //variables to measure the time of a loop
bool err_Calculated=false;                   //True if error is yet calculated
int16_t Gyr_rawZ;                            //Raw value of the angle
float Gyr_angle_z;                           //Value of the angle
float Gyr_raw_err_z;                         //Error on the raw value
CircBuffer values;                           //Circbuffer with the most recent angle values
float oldAngle, newAngle, angleShift, avg;   //Extra variables to make sure only data will be sent to the decoder if necessary

void setup() {
  //MPU6050 init
  Wire.begin();
  
  Wire.beginTransmission(MPU);   //Begin transmission to the MPU6050
  Wire.write(0x6B);              //Write to the power management register
  Wire.write(0x00);              //Reset
  Wire.endTransmission(true);

  Wire.beginTransmission(MPU);
  Wire.write(0x1B);              //Write to gyroscope config register
  Wire.write(0x08);              //Set full scale range to 500 degrees per second
  Wire.endTransmission(true);

  Serial.begin(9600);
  time=millis();

  //Start calculating the error with 200 samples
  if(err_Calculated==false)
  {
    for(int i=0; i<200; i++)
    {
      Wire.beginTransmission(0x68);            //begin, Send the slave adress (in this case 68) 
      Wire.write(0x47);                        //First adress of the Gyro z data
      Wire.endTransmission(false);
      Wire.requestFrom(MPU,2,true);           // Only rotation around z-axis 
         
      Gyr_rawZ=Wire.read()<<8|Wire.read();
  
      Gyr_raw_err_z = Gyr_raw_err_z + (Gyr_rawZ/65.5);  //Divide by 65.5 because datasheet says so when using a scale range of 500 degrees per second
      
      //Calculation stops here
      if(i==199)
      {
        Gyr_raw_err_z = Gyr_raw_err_z/200;
        err_Calculated=true;
      }
    }
  } 
  //Circular buffer init of length 50
  values.init(50);

  //Set analog reference to 1.1V via internal
  analogReference(INTERNAL);
  //Make batteryPin analog input and batteryLed digital output
  pinMode(batteryLed, OUTPUT);
  pinMode(batteryPin, INPUT);
}

void loop() {
  //Timer to count the time used for one loop  
  timePrev = time;
  time = millis();
  elapsedTime = (time-timePrev)/1000;

  Wire.beginTransmission(MPU);
  Wire.write(0x47);
  Wire.endTransmission(false);
  Wire.requestFrom(MPU, 2, true);                 //Request raw data

  Gyr_rawZ = Wire.read()<<8|Wire.read();          //Read Raw value
  Gyr_rawZ = (Gyr_rawZ/65.5) - Gyr_raw_err_z;     //Update raw value
  Gyr_angle_z += Gyr_rawZ*elapsedTime;            //Get the angle difference by multiplying the raw value with the elapsed time
  
  /*We want to use values in the interval [0, 360], so we will do the following*/
  Gyr_angle_z = fmod(Gyr_angle_z, 360);
  while (Gyr_angle_z < 0) Gyr_angle_z +=360; 
  values.put(Gyr_angle_z);                        //Put value in buffer

  /*Looking for a changement in value by calculating the difference between constant signals*/
  if(abs(values.getAverage() - Gyr_angle_z) <= 0.01){   //Check if values are the same
    oldAngle = newAngle;
    newAngle = Gyr_angle_z;
    angleShift = newAngle - oldAngle;
    if (angleShift<-180) angleShift += 360;
    else if (angleShift>180) angleShift -= 360;
    if (abs(angleShift) >= 11.25){
      Serial.println(angleShift);
    }
  }

  //Check if the battery voltage is high enough >5V
  if(analogRead(batteryPin)<0.45){
    digitalWrite(batteryLed, HIGH);
  }
}
```