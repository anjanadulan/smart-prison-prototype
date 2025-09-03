# 🔌 Smart Prison System - Code Modules

This repository contains the source code for **two major subsystems** of the Smart Prison Management System prototype:

1. **Alarm System** – Smoke, temperature, and light detection with alerting.
2. **Light System (without automative motion detecting)** – Automatic indoor and outdoor lighting using LDR sensors.

---

## 📁 Code Description

| File | Description |
|-------|-------------|
| `Alarm system` | Handles smoke detection, high-temperature alarms, and darkness detection with LEDs and buzzers. |
| `Light system` | Controls indoor and outdoor lighting based on environmental light conditions. |

---

## 1️⃣ Alarm System

### **Features**
- Detects **smoke/gas** with the MQ-2 sensor.
- Detects **high temperature** with a temperature sensor.
- Detects **low light** with an LDR sensor.
- Provides alerts using:
  - **Buzzers** for alarms.
  - **LEDs** for light status.
  - **Serial Monitor** logs for debugging and status updates.

### **Key Pins**
| Sensor/Component | Pin |
|------------------|------|
| Smoke Sensor (MQ-2) | D2 |
| Smoke Logic Out | D8 |
| Temperature Sensor | D3 |
| Temperature Logic Out | D9 |
| LDR Sensor | A0 |
| LDR Logic Out | D10 |

### **Code**
```cpp
const int smokePin = 2;      // DO pin from MQ-2
const int sOut = 8;     // Buzzer

const int tempPin = 3;       // Digital Output from module
const int tOut = 9;     // Buzzer pin

const int ldrPin = A0; // Connect LDR module's AO pin to Arduino's A0
const int ledPin = 10;  // Connect an LED to digital pin 9 (with a current-limiting resistor)
const int threshold = 500; // Adjust this value based on your environment and desired sensitivity

void setup() {
  pinMode(smokePin, INPUT);
  pinMode(sOut, OUTPUT);

  pinMode(tempPin, INPUT);
  pinMode(tOut, OUTPUT);
  digitalWrite(tOut, LOW);
  Serial.begin(9600);

  pinMode(ldrPin, INPUT);
  pinMode(ledPin, OUTPUT); // Set the LED pin as an output
}

void loop() {
  int smokeState = digitalRead(smokePin);
  int tempStatus = digitalRead(tempPin);

  if (smokeState == LOW) {
    digitalWrite(sOut, HIGH);
    Serial.println("🚨 Smoke or gas detected!");
    delay(1000);
  } else {
    digitalWrite(sOut, LOW);
    Serial.println("✅ Air is clean.");
  }

  if (tempStatus == LOW) {
    digitalWrite(tOut, HIGH);
    Serial.println("Temperature TOO HIGH!");
    delay(1000);
  } else {
    digitalWrite(tOut, LOW);
    Serial.println("Temperature Normal");
  }

  int ldrValue = analogRead(ldrPin);
  Serial.print("LDR Value: ");
  Serial.println(ldrValue);

  if (ldrValue <= threshold) {
    digitalWrite(ledPin, HIGH);
    Serial.println("Darkness detected, LED ON");
  } else {
    digitalWrite(ledPin, LOW);
    Serial.println("Sufficient light, LED OFF");
  }
  delay(100);
}
```

---

## 2️⃣ Light System (without automative motion detecting)

### **Features**
- Controls **indoor** and **outdoor** lighting using **LDR sensors**.
- Automatically turns LEDs ON in darkness and OFF in sufficient light.
- Logs sensor readings for monitoring via Serial Monitor.

### **Key Pins**
| Sensor/Component | Pin |
|------------------|------|
| Indoor LDR Sensor | A0 |
| Indoor Logic Out | D8 |
| Outdoor LDR Sensor | A1 |
| Outdoor Logic Out | D9 |

### **Code**
```cpp
const int threshold = 500; // Adjust this value based on your environment and desired sensitivity

// Indoor Light System
const int ldrPin = A0; // Connect LDR module's AO pin to Arduino's A0
const int ledPin = 8;  // Connect an LED to digital pin 8 (with a current-limiting resistor)

// Outdoor Light System
const int ldrPin2 = A1; // Connect LDR module's A1 pin to Arduino's A0
const int ledPin2 = 9;  // Connect an LED to digital pin 9 (with a current-limiting resistor)

void setup() {
  Serial.begin(9600);
  pinMode(ldrPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(ldrPin2, INPUT);
  pinMode(ledPin2, OUTPUT);
}

void loop() {
  // Indoor Light Condition
  int ldrValue = analogRead(ldrPin);
  Serial.print("LDR Value: ");
  Serial.println(ldrValue);

  if (ldrValue >= threshold) {
    digitalWrite(ledPin, HIGH);
    Serial.println("Darkness detected, LED ON");
  } else {
    digitalWrite(ledPin, LOW);
    Serial.println("Sufficient light, LED OFF");
  }

  // Outdoor Light Condition
  int ldrValue2 = analogRead(ldrPin2);
  Serial.print("LDR Value: ");
  Serial.println(ldrValue2);

  if (ldrValue2 >= threshold) {
    digitalWrite(ledPin2, HIGH);
    Serial.println("Darkness detected, LED2 ON");
  } else {
    digitalWrite(ledPin2, LOW);
    Serial.println("Sufficient light, LED2 OFF");
  }
  delay(100);
}
```

---

