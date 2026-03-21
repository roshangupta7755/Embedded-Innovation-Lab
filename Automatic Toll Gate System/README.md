<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00C9FF,100:92FE9D&height=200&section=header&text=Automatic%20Toll%20Gate%20System&fontSize=36&fontColor=ffffff&fontAlignY=38&desc=Embedded%20Systems%20%7C%20Arduino%20%7C%20Real-Time%20Automation&descSize=16&descAlignY=58&animation=fadeIn" width="100%"/>

<br/>

[![Arduino](https://img.shields.io/badge/Platform-Arduino_Uno-00979D?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Language](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)](https://isocpp.org/)
[![Domain](https://img.shields.io/badge/Domain-Embedded_Systems-FF6F00?style=for-the-badge)](https://en.wikipedia.org/wiki/Embedded_system)
[![Status](https://img.shields.io/badge/Build-Passing-brightgreen?style=for-the-badge&logo=githubactions&logoColor=white)](https://github.com/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

<br/>

> **A hardware-driven toll gate automation system leveraging ultrasonic sensing, servo actuation, and LED signaling — engineered on Arduino Uno.**

<br/>

</div>

---

<div align="center">

### `[ Detection ]` → `[ Processing ]` → `[ Gate Control ]` → `[ Visual Signal ]`

</div>

---

## 📡 Overview

The **Automatic Toll Gate System** is a real-time embedded solution designed to eliminate manual toll operation. When a vehicle enters the detection zone, the ultrasonic sensor captures proximity data, the Arduino processes the signal, and the servo motor actuates the gate — all within milliseconds. LED indicators provide instant visual feedback.

This project demonstrates the complete hardware-software integration cycle: from raw sensor data to a physical, real-world mechanical response.

---

## 🚀 Highlights

<table>
<tr>
<td>⚡</td>
<td><strong>Instant Detection</strong></td>
<td>HC-SR04 ultrasonic sensor detects vehicles within a configurable distance threshold</td>
</tr>
<tr>
<td>🔄</td>
<td><strong>Auto Gate Actuation</strong></td>
<td>SG90 servo rotates 90° to open / 0° to close with millisecond precision</td>
</tr>
<tr>
<td>🟢</td>
<td><strong>Dual LED Signaling</strong></td>
<td>Green LED for gate-open state, Red LED for gate-closed state</td>
</tr>
<tr>
<td>⏱️</td>
<td><strong>Timed Auto-Close</strong></td>
<td>Gate remains open for a configurable duration, then closes automatically</td>
</tr>
<tr>
<td>🔁</td>
<td><strong>Continuous Loop</strong></td>
<td>Real-time polling loop — no manual resets or interrupts required</td>
</tr>
<tr>
<td>🔌</td>
<td><strong>Prototype-Ready</strong></td>
<td>Fully breadboard-compatible; buildable in under 30 minutes</td>
</tr>
</table>

---

## 🧰 Tech Stack

<div align="center">

[![Arduino Uno](https://img.shields.io/badge/Arduino_Uno-ATmega328P-00979D?style=flat-square&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![HC-SR04](https://img.shields.io/badge/Sensor-HC--SR04_Ultrasonic-0077B6?style=flat-square)](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)
[![SG90](https://img.shields.io/badge/Actuator-SG90_Servo_Motor-FF6F00?style=flat-square)](https://components101.com/motors/servo-motor-basics-pinout-datasheet)
[![LED](https://img.shields.io/badge/Output-LED_Indicators_(R%2FG)-FF0000?style=flat-square)](https://en.wikipedia.org/wiki/Light-emitting_diode)
[![C++](https://img.shields.io/badge/Code-Arduino_C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white)](https://isocpp.org/)
[![Breadboard](https://img.shields.io/badge/Prototype-Breadboard_Circuit-6C757D?style=flat-square)](https://en.wikipedia.org/wiki/Breadboard)

</div>

---

## ⚙️ How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                        SYSTEM FLOW                              │
│                                                                 │
│   [START] ──▶ Ultrasonic Pulse Emitted                          │
│                        │                                        │
│                        ▼                                        │
│            Echo Received by HC-SR04                             │
│                        │                                        │
│                        ▼                                        │
│         Arduino Calculates Distance (cm)                        │
│                        │                                        │
│             ┌──────────┴──────────┐                             │
│             ▼                     ▼                             │
│      Distance < 15cm        Distance ≥ 15cm                     │
│             │                     │                             │
│             ▼                     ▼                             │
│      GATE OPENS (90°)       GATE STAYS CLOSED (0°)              │
│      Green LED ON           Red LED ON                          │
│             │                                                   │
│             ▼                                                   │
│      Wait 3 seconds                                             │
│             │                                                   │
│             ▼                                                   │
│      GATE CLOSES (0°) ──▶ Red LED ON ──▶ [LOOP]                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔌 Circuit Connections

```
HC-SR04 Ultrasonic Sensor          Arduino Uno
──────────────────────────         ───────────
VCC          ─────────────────▶    5V
GND          ─────────────────▶    GND
TRIG         ─────────────────▶    Digital Pin 9
ECHO         ─────────────────▶    Digital Pin 10

SG90 Servo Motor                   Arduino Uno
────────────────                   ───────────
VCC (Red)    ─────────────────▶    5V
GND (Brown)  ─────────────────▶    GND
SIG (Orange) ─────────────────▶    Digital Pin 6 (PWM)

Green LED                          Arduino Uno
─────────                          ───────────
Anode (+)  ──▶ 220Ω ─────────▶    Digital Pin 4
Cathode (−)  ─────────────────▶    GND

Red LED                            Arduino Uno
───────                            ───────────
Anode (+)  ──▶ 220Ω ─────────▶    Digital Pin 3
Cathode (−)  ─────────────────▶    GND
```

---

## 📂 Code Structure

```cpp
// ═══════════════════════════════════════════════════════
//  Automatic Toll Gate System
//  Platform : Arduino Uno (ATmega328P)
//  Language : C++ (Arduino Framework)
// ═══════════════════════════════════════════════════════

#include <Servo.h>

// ── Pin Configuration ───────────────────────────────────
#define TRIG_PIN            9
#define ECHO_PIN            10
#define SERVO_PIN           6
#define GREEN_LED           4
#define RED_LED             3

// ── System Parameters ───────────────────────────────────
#define DETECT_THRESHOLD_CM 15
#define GATE_OPEN_DELAY_MS  3000

Servo gateServo;

// ── Setup ────────────────────────────────────────────────
void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  gateServo.attach(SERVO_PIN);
  gateServo.write(0);
  digitalWrite(RED_LED, HIGH);
  Serial.begin(9600);
}

// ── Distance Measurement ─────────────────────────────────
long measureDistance() {
  digitalWrite(TRIG_PIN, LOW);  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH); delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  return pulseIn(ECHO_PIN, HIGH) * 0.034 / 2;
}

// ── Gate Control ─────────────────────────────────────────
void openGate()  {
  gateServo.write(90);
  digitalWrite(GREEN_LED, HIGH);
  digitalWrite(RED_LED, LOW);
}

void closeGate() {
  gateServo.write(0);
  digitalWrite(GREEN_LED, LOW);
  digitalWrite(RED_LED, HIGH);
}

// ── Main Loop ─────────────────────────────────────────────
void loop() {
  long dist = measureDistance();
  Serial.print("Distance: "); Serial.print(dist); Serial.println(" cm");
  if (dist > 0 && dist < DETECT_THRESHOLD_CM) {
    openGate();
    delay(GATE_OPEN_DELAY_MS);
    closeGate();
  }
  delay(100);
}
```

---

## 🧩 Components

| Component | Model | Role |
|---|---|---|
| Microcontroller | Arduino Uno (ATmega328P) | Core logic & GPIO control |
| Ultrasonic Sensor | HC-SR04 | Vehicle proximity detection |
| Servo Motor | SG90 (0–180°) | Gate open/close actuation |
| Green LED | 5mm Standard | Gate-open visual indicator |
| Red LED | 5mm Standard | Gate-closed visual indicator |
| Resistors | 220Ω × 2 | LED current limiting |
| Breadboard + Jumpers | Standard | Prototyping & wiring |
| Power Source | USB / 5V DC | System power supply |

---

## 🎥 Demo / Preview

<div align="center">

**▶ [Watch the Project Demo on LinkedIn](https://www.linkedin.com/)**

</div>

The demo video covers:
- Live vehicle detection using the ultrasonic sensor
- Real-time servo gate actuation (open → wait → close)
- LED state transitions synchronized with gate position
- Serial monitor output showing live distance readings

---

## 📚 Learning Outcomes

- **Sensor Integration** — Reading and interpreting HC-SR04 ultrasonic data via digital GPIO
- **Actuator Control** — PWM-based servo motor angular positioning
- **Embedded C++** — Clean, modular Arduino programming with `#define` constants and function separation
- **Circuit Design** — Designing and wiring a multi-component embedded prototype
- **System Timing** — Implementing reliable delay-based gate sequencing
- **Hardware Debugging** — Using `Serial.print()` for real-time diagnostics

---

## 🔮 Future Scope

- [ ] **RFID / NFC** — Identify vehicles, automate toll deduction, reject unauthorized entries
- [ ] **IoT Integration** — Stream gate events to a cloud dashboard via ESP8266 / ESP32
- [ ] **LCD Display** — On-site status display showing vehicle count and gate state
- [ ] **IR Redundancy** — Add IR sensors for multi-point vehicle confirmation
- [ ] **Camera Module** — Log vehicle entry images for audit and security
- [ ] **PCB Design** — Convert the breadboard prototype to a production-grade custom PCB
- [ ] **Solar Power** — Enable off-grid deployment for rural toll infrastructure
- [ ] **Mobile Alerts** — Push system fault notifications to an operator app

---

## 👨‍💻 Developer

<div align="center">

**Built with precision, curiosity, and a love for embedded systems.**

<br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:your@email.com)

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:92FE9D,100:00C9FF&height=100&section=footer" width="100%"/>

**⭐ Star this repo if it sparked something — it means the world!**

*`while(alive) { learn(); build(); repeat(); }`*

</div>
