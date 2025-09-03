# 🔍 System Logic Overview

The **Smart Prison Management System** uses basic digital logic combined with Arduino sensors.  
Each subsystem works based on the following truth tables and simplified logic expressions:

---

## 1️⃣ Prison Cage Light System
**Logic:** Lights turn ON automatically when it’s dark or manually via a switch.

| Light Sensor (SL) | Switch (SW) | Cage Light (CL) |
|------------------|-------------|-----------------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

**Simplified Expression:**  
CL = SL + SW

---


## 2️⃣ Prison Corridor Light System
**Logic:** Corridor lights turn ON with motion during darkness or via manual override.

| Light (SL) | Motion (MO) | Switch (SW) | Corridor Light (CL) |
|-------------|-------------|-------------|----------------------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

**Simplified Expression:**  
CL = SW + (SL' * MO)

---


## 3️⃣ Outdoor Light System
**Logic:** Outdoor lights work similar to corridor lights, with motion detection and manual override.

| Light (SL) | Motion (MO) | Switch (SW) | Outdoor Light (OL) |
|-------------|-------------|-------------|---------------------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

**Simplified Expression:**  
OL = SW + (SL' * MO)

---


## 4️⃣ Security Alarm System
**Logic:** Alarm triggers when a door opens without permission or when the manual override is ON.

| Door Switch (Dsw) | Door Motion (Dm) | Manual SW (SW) | Alarm (AS) |
|-------------------|------------------|----------------|-------------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

**Simplified Expression:**  
AS = SW + (Dm * Dsw')

---


## 5️⃣ Fire Alarm System
**Logic:** Alarm triggers if smoke or high temperature is detected, or if manual override is pressed.

| Smoke (SD) | Temp (TEMP) | Switch (SW) | Fire Alarm (AF) |
|-------------|-------------|-------------|-----------------|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

**Simplified Expression:**  
AF = SW + (SD * TEMP)

"""
