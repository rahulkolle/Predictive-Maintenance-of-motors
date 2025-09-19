# Predictive Maintenance of Motors

This project is designed to **predict and prevent motor failures** by monitoring critical parameters such as **temperature, humidity, and vibration** in real-time. The system helps avoid breakdowns by sending alerts when the motor operates outside safe thresholds.

---

## 🚀 Features
- Real-time monitoring of motor health.
- Uses **Arduino** with multiple sensors:
  - Temperature Sensor (to detect overheating)
  - Humidity Sensor (for environment conditions)
  - Vibration Sensor (to detect abnormal vibrations)
- Threshold-based alert system.
- Buzzer/Notification alert when unsafe values are detected.
- Prevents downtime and reduces maintenance cost.

---

## 🛠️ Hardware Components
- Arduino Uno (or compatible board)
- DHT11/DHT22 (Temperature & Humidity sensor)
- Vibration Sensor (e.g., SW-420)
- Buzzer for alert
- Motor setup
- Jumper wires, breadboard, power supply

---

## 📂 Project Workflow
1. Sensors continuously collect data from the motor.
2. Arduino processes the data and compares it with predefined thresholds.
3. If values exceed safe limits:
   - A buzzer alert is triggered.
   - A notification can be sent (via connected module).
4. User can shut down the motor to prevent damage.

---

---

## 💻 Arduino Code (Sample)
```cpp
#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11
#define VIBRATION_PIN 3
#define BUZZER 4

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  pinMode(VIBRATION_PIN, INPUT);
  pinMode(BUZZER, OUTPUT);
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  float temp = dht.readTemperature();
  float humidity = dht.readHumidity();
  int vibration = digitalRead(VIBRATION_PIN);

  Serial.print("Temp: "); Serial.print(temp);
  Serial.print("°C  Humidity: "); Serial.print(humidity);
  Serial.print("%  Vibration: "); Serial.println(vibration);

  if (temp > 60 || humidity > 80 || vibration == HIGH) {
    digitalWrite(BUZZER, HIGH);
  } else {
    digitalWrite(BUZZER, LOW);
  }

  delay(2000);
}

