//parking-sensor
//This project utilizes the ESP32 microcontroller for an embedded system aimed at enhancing road safety. The user-friendly interface ensures seamless communication between hardware and software, providing non-intrusive alerts for drivers. The system prioritizes safety when driving. 

#include <Wire.h>
#define echoPin 2
#define trigPin 15
#define ledRPin 0
#define ledYPin 4
#define ledGPin 16

long duration, distance; 
void setup(){
  Serial.begin (9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledRPin, OUTPUT);
  pinMode(ledYPin, OUTPUT);
  pinMode(ledGPin, OUTPUT);
}

void loop(){
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration / 58.2;
  String disp = String(distance);

  Serial.print("Distance: ");
  Serial.print(disp);
  Serial.println(" cm");
  delay(10);


  if (distance >= 0 && distance <= 10) {
    digitalWrite(ledRPin, HIGH);
    digitalWrite(ledYPin, LOW);
    digitalWrite(ledGPin, LOW);
  } else if (distance > 10 && distance <= 20) {
    digitalWrite(ledRPin, LOW);
    digitalWrite(ledYPin, HIGH);
    digitalWrite(ledGPin, LOW);
  } else if (distance > 20 && distance <= 30) {
    digitalWrite(ledRPin, LOW);
    digitalWrite(ledYPin, LOW);
    digitalWrite(ledGPin, HIGH);
  } else {
    digitalWrite(ledRPin, LOW);
    digitalWrite(ledYPin, LOW);
    digitalWrite(ledGPin, LOW);
  }
}
