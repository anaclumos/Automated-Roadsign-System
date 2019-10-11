# Automated Roadsign System

### Note: This project is from June ~ July 2017.

This is an Automated Roadsign System that can handle efficient traffic management with audial assistance. It is simulated with Arduino Uno and a custom designed circuit board (designed by myself!)

|Presentations|Content|Link|
|----|----|----|
|Mid Presentation|**idea** of the project|[resources/Mid/README.md](resources/Mid/README.md)|
|Fin Presentation|**results** of the project|[resources/Fin/README.md](resources/Fin/README.md)|

![`Circuit Designs`](resources/Circuit.jpg)

## Demo Video
[![Automated Roadsign System Demo Video on YouTube](http://img.youtube.com/vi/VWpHIZOT2t8/0.jpg)](https://youtu.be/VWpHIZOT2t8)

## [RoadSign.ino](RoadSign.ino)
```ino
boolean val1, val2;
const int laser1 = 2;
const int led1gre = 3;
const int led1leg = 4;
const int led1red = 5;
const int buz1gro = 6;
const int buz1sky = 7;
const int buz2gro = 8;
const int buz2sky = 9;
const int led2gre = 10;
const int led2leg = 11;
const int led2red = 12;
const int laser2 = 13;

void setup()
{
  Serial.begin(9600);
  pinMode(laser1, INPUT);
  pinMode(laser2, INPUT);
  pinMode(led1gre, OUTPUT);
  pinMode(led1leg, OUTPUT);
  pinMode(led1red, OUTPUT);
  pinMode(buz1gro, OUTPUT);
  pinMode(buz1sky, OUTPUT);
  pinMode(buz2gro, OUTPUT);
  pinMode(buz2sky, OUTPUT);
  pinMode(led2gre, OUTPUT);
  pinMode(led2leg, OUTPUT);
  pinMode(led2red, OUTPUT);
  digitalWrite(led1gre, LOW);
  digitalWrite(led1leg, LOW);
  digitalWrite(led1red, HIGH);
  digitalWrite(buz1gro, LOW);
  digitalWrite(buz1sky, LOW);
  digitalWrite(buz2gro, LOW);
  digitalWrite(buz2sky, LOW);
  digitalWrite(led2gre, LOW);
  digitalWrite(led2leg, LOW);
  digitalWrite(led2red, HIGH);
}

void loop()
{

  val1 = digitalRead(laser1);
  val2 = digitalRead(laser2);
  Serial.println("val1 : " + (String)val1 + " val2 : " + (String)val2);

  if (!val1)
  {
    Serial.println("RoadSign 1 detected an object");
    digitalWrite(buz1sky, HIGH);
    delay(500);
    digitalWrite(buz1sky, LOW);
    delay(1000);
    for (int i = 0; i < 5; i++)
    {
      digitalWrite(led1red, LOW);
      digitalWrite(led1gre, HIGH);
      digitalWrite(led2red, LOW);
      digitalWrite(led2gre, HIGH);
      digitalWrite(buz1sky, HIGH);
      delay(300);
      digitalWrite(buz1sky, LOW);
      delay(300);
      digitalWrite(buz2sky, HIGH);
      delay(140);
      digitalWrite(buz2sky, LOW);
      delay(20);
      digitalWrite(buz2sky, HIGH);
      delay(140);
      digitalWrite(buz2sky, LOW);
      delay(20);
      delay(300);
    }
  }

  else
  {
    digitalWrite(led1gre, LOW);
    digitalWrite(led1red, HIGH);
  }

  if (!val2)
  {
    Serial.println("RoadSign 2 detected an object");
    digitalWrite(buz2sky, HIGH);
    delay(140);
    digitalWrite(buz2sky, LOW);
    delay(20);
    digitalWrite(buz2sky, HIGH);
    delay(140);
    digitalWrite(buz2sky, LOW);
    delay(3000);
    for (int i = 0; i < 5; i++)
    {
      digitalWrite(led2red, LOW);
      digitalWrite(led2gre, HIGH);
      digitalWrite(led1red, LOW);
      digitalWrite(led1gre, HIGH);
      digitalWrite(buz2sky, HIGH);
      delay(140);
      digitalWrite(buz2sky, LOW);
      delay(20);
      digitalWrite(buz2sky, HIGH);
      delay(140);
      digitalWrite(buz2sky, LOW);
      delay(300);
      digitalWrite(buz1sky, HIGH);
      delay(300);
      digitalWrite(buz1sky, LOW);
      delay(300);
    }
  }

  else
  {
    digitalWrite(led2gre, LOW);
    digitalWrite(led2red, HIGH);
  }
}
```
