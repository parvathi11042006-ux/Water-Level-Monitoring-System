# Water Level Monitoring System

## Aim

To design and implement a Water Level Monitoring System using Arduino to monitor the water level in a tank and indicate the water status through LEDs.

---

## Components Required

- Arduino Uno
- Water Level Sensor
- Red LED
- Yellow LED
- Green LED
- 220Ω Resistors (3)
- Breadboard
- Jumper Wires
- USB Cable

---

## Program

#define trigPin 9
#define echoPin 10

#define greenLED 3
#define yellowLED 4
#define redLED 5

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);

  distance = duration * 0.034 / 2;

  Serial.print("Water Level Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance > 70) {
    // Low water level
    digitalWrite(redLED, HIGH);
    digitalWrite(yellowLED, LOW);
    digitalWrite(greenLED, LOW);
  }
  else if (distance > 30 && distance <= 70) {
    digitalWrite(redLED, LOW);
    digitalWrite(yellowLED, HIGH);
    digitalWrite(greenLED, LOW);
  }
  else {
    // High water level
    digitalWrite(redLED, LOW);
    digitalWrite(yellowLED, LOW);
    digitalWrite(greenLED, HIGH);
  }

  delay(500);
}


---

## Result

The Water Level Monitoring System was successfully implemented using Arduino and a Water Level Sensor. The system monitored the water level accurately and indicated low, medium, and high water levels using LEDs. The water level readings were also displayed in the Serial Monitor.

---
