# ⚙️ DC Motor Speed Control using PWM with Obstacle Detection

## 📌 Project Overview
This project demonstrates how to control the speed of a DC motor using PWM (Pulse Width Modulation) and automatically stop the motor when an obstacle is detected using an ultrasonic sensor (HC-SR04).

---

## 🎯 Features
- 🔄 PWM-based motor speed control  
- 📡 Real-time distance measurement  
- 🚫 Automatic obstacle detection and motor stop  
- ⚡ Efficient embedded control system  

---

## 🧰 Hardware Components
- Arduino UNO / ESP32  
- L293D Motor Driver / L298N  
- DC Motor  
- HC-SR04 Ultrasonic Sensor  
- Power Supply  
- Jumper wires  

---

## 🔌 Circuit Diagram
![Circuit Diagram](images/circuit.png)

---

## ⚙️ Working Principle
1. Ultrasonic sensor sends sound waves  
2. Echo signal is received and time is measured  
3. Distance is calculated  
4. PWM signal controls motor speed  
5. If distance > 20 cm → Motor runs  
6. If distance ≤ 20 cm → Motor stops  

---

## 💻 Code

```cpp
#define ENA 5
#define IN1 8
#define IN2 9

#define TRIG 10
#define ECHO 11

long duration;
int distance;

int speedValue = 180;
int threshold = 20;

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);

  Serial.begin(9600);
}

void loop() {
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  duration = pulseIn(ECHO, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > threshold) {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    analogWrite(ENA, speedValue);

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm | MOTOR: ON");
  } else {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    analogWrite(ENA, 0);

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm | MOTOR: OFF");
  }

  delay(200);
}

##📊 Results
Distance (cm)	Motor Status
30	ON
25	ON
21	ON
15	OFF
10	OFF

##🚀 How to Run
Connect components as per circuit diagram
Open Arduino IDE
Select correct board and port
Upload code
Open Serial Monitor
Observe motor behavior

##📈 Observations
Motor runs smoothly at safe distance
Motor stops when obstacle is detected
System responds quickly

##⚡ Advantages
Low cost
Easy implementation
Energy efficient
Reliable operation

##🔮 Future Improvements
PID-based speed control
Distance-based variable speed
Buzzer alert system
Wireless control using ESP32
