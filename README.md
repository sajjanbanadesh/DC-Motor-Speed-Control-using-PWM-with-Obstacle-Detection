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
- 
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
## 📊 Results

| Distance (cm) | Motor Status |
|--------------|-------------|
| 30           | ON          |
| 25           | ON          |
| 21           | ON          |
| 15           | OFF         |
| 10           | OFF         |

---

## 🚀 How to Run

1. Connect components as per the circuit diagram  
2. Open Arduino IDE  
3. Select the correct board and port  
4. Upload the code to Arduino/ESP32  
5. Open Serial Monitor  
6. Observe distance readings and motor behavior  

---

## 📈 Observations

- Motor runs smoothly when no obstacle is present  
- Motor stops immediately when an obstacle is detected  
- System responds quickly to distance changes  
- Threshold (~20 cm) works effectively  

---

## ⚡ Advantages

- Low cost and simple design  
- Easy to implement  
- Energy efficient  
- Reliable and real-time operation  

---

## 🔮 Future Improvements

- Implement PID-based speed control  
- Add distance-based variable speed control  
- Integrate buzzer for alert system  
- Enable wireless control using ESP32/WiFi  
