<div align="center">

# ⚡ Automatic Toll Gate System

### *Smart Infrastructure. Zero Delays. Pure Automation.*

[![Arduino](https://img.shields.io/badge/Platform-Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![C++](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)](https://isocpp.org/)
[![Embedded Systems](https://img.shields.io/badge/Domain-Embedded%20Systems-FF6F00?style=for-the-badge&logo=embeddedartistry&logoColor=white)](https://en.wikipedia.org/wiki/Embedded_system)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)](https://github.com/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

> **Automating toll collection through real-time vehicle detection, servo-controlled gate actuation, and LED-based visual signaling — built entirely on Arduino.**

</div>

---

## 📌 Table of Contents

- [Why This Project Matters](#-why-this-project-matters)
- [Highlights](#-highlights)
- [Features](#-features)
- [System Architecture](#-system-architecture)
- [How It Works](#-how-it-works)
- [Components Used](#-components-used)
- [Circuit Overview](#-circuit-overview)
- [Code Structure](#-code-structure)
- [Project Images](#-project-images)
- [Demo](#-demo--preview)
- [Learning Outcomes](#-learning-outcomes)
- [Future Scope](#-future-scope)
- [Connect](#-connect)

---

## 💡 Why This Project Matters

Manual toll collection is a bottleneck in modern transportation — causing traffic congestion, human error, and inefficiency. This project presents a **low-cost, hardware-driven automation solution** that can:

- Eliminate the need for manual gate operators
- Reduce vehicle wait times at toll plazas
- Serve as a foundation for **RFID or IoT-integrated smart toll systems**
- Demonstrate real-world embedded systems thinking at the intersection of hardware and software

Whether you're a student, a maker, or a recruiter — this project showcases practical engineering that solves a genuine infrastructure problem.

---

## 🚀 Highlights

- 🔴 **Real-time detection** using HC-SR04 Ultrasonic Sensor
- 🔁 **Automated gate control** via SG90 Servo Motor
- 🟢 **Dual LED signaling** for visual vehicle status feedback
- ⚡ **Instant actuation** — gate opens/closes within milliseconds of detection
- 🧠 **Pure Arduino logic** — no external libraries, no black boxes
- 🔌 **Fully breadboard-compatible** — easy to build and prototype

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎯 Vehicle Detection | HC-SR04 ultrasonic sensor detects approaching vehicles within a configurable threshold range |
| 🔄 Auto Gate Control | Servo motor rotates to open (90°) or close (0°) the gate based on detection |
| 🟢 Green LED | Illuminates when vehicle is detected and gate is open — safe to proceed |
| 🔴 Red LED | Illuminates when no vehicle is present and gate is closed — access restricted |
| ⏱️ Timed Gate Operation | Gate stays open for a set duration, then automatically closes |
| 🔁 Continuous Loop | System runs in a real-time polling loop — no manual resets needed |

---

## 🧩 System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   ARDUINO UNO (Brain)                   │
│                                                         │
│  ┌─────────────┐    ┌──────────────┐   ┌─────────────┐ │
│  │  Ultrasonic │    │ Servo Motor  │   │  LED Module │ │
│  │   Sensor    │───▶│  (Gate Ctrl) │   │ (R/G Signal)│ │
│  │  HC-SR04    │    │    SG90      │   │             │ │
│  └──────┬──────┘    └──────┬───────┘   └──────┬──────┘ │
│         │                  │                   │        │
│    [TRIG / ECHO]      [PWM Signal]        [Digital I/O] │
│         │                  │                   │        │
│         └──────────────────▼───────────────────▘        │
│                      Arduino GPIO                       │
└─────────────────────────────────────────────────────────┘

Detection Flow:
  Vehicle Detected → Gate Opens → Green LED ON → Wait → Gate Closes → Red LED ON
```

---

## ⚙️ How It Works

```
Step 1 ──▶ Ultrasonic sensor emits a sound pulse every loop cycle

Step 2 ──▶ Pulse reflects off vehicle surface and returns to sensor

Step 3 ──▶ Arduino calculates distance using travel time of sound

Step 4 ──▶ If distance < threshold (e.g., 15 cm):
            └──▶ Servo rotates to 90° (gate OPENS)
            └──▶ Green LED turns ON
            └──▶ Red LED turns OFF

Step 5 ──▶ Gate remains open for a defined delay period

Step 6 ──▶ Servo rotates back to 0° (gate CLOSES)
            └──▶ Green LED turns OFF
            └──▶ Red LED turns ON

Step 7 ──▶ System returns to Step 1 — continuous polling
```

---

## 🧰 Components Used

| Component | Model | Purpose |
|---|---|---|
| Microcontroller | Arduino Uno (ATmega328P) | Central processing & control logic |
| Ultrasonic Sensor | HC-SR04 | Vehicle proximity detection |
| Servo Motor | SG90 (180°) | Physical gate actuation |
| LED (Green) | 5mm Standard | Visual signal — gate open / vehicle detected |
| LED (Red) | 5mm Standard | Visual signal — gate closed / no vehicle |
| Resistors | 220Ω | Current limiting for LEDs |
| Power Supply | USB / 5V DC | System power |
| Breadboard + Jumpers | — | Prototyping & connections |

---

## 🔌 Circuit Overview

```
HC-SR04 Ultrasonic Sensor:
  VCC   ──▶  5V
  GND   ──▶  GND
  TRIG  ──▶  Digital Pin 9
  ECHO  ──▶  Digital Pin 10

SG90 Servo Motor:
  VCC   ──▶  5V
  GND   ──▶  GND
  SIG   ──▶  Digital Pin 6 (PWM)

Green LED:
  Anode (+)  ──▶  220Ω Resistor ──▶  Digital Pin 4
  Cathode (−)──▶  GND

Red LED:
  Anode (+)  ──▶  220Ω Resistor ──▶  Digital Pin 3
  Cathode (−)──▶  GND
```

---

## 🖥️ Code Structure

```cpp
// ── Automatic Toll Gate System ──────────────────────────
// Author  : [Your Name]
// Platform: Arduino Uno
// Language: C++ (Arduino Framework)
// ────────────────────────────────────────────────────────

#include <Servo.h>

// Pin Definitions
#define TRIG_PIN    9
#define ECHO_PIN    10
#define SERVO_PIN   6
#define GREEN_LED   4
#define RED_LED     3

// Configuration
#define DETECT_THRESHOLD_CM  15
#define GATE_OPEN_DELAY_MS   3000

Servo gateServo;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  gateServo.attach(SERVO_PIN);
  gateServo.write(0);         // Gate closed on boot
  digitalWrite(RED_LED, HIGH);
  Serial.begin(9600);
}

long measureDistance() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  long duration = pulseIn(ECHO_PIN, HIGH);
  return duration * 0.034 / 2;
}

void openGate() {
  gateServo.write(90);
  digitalWrite(GREEN_LED, HIGH);
  digitalWrite(RED_LED, LOW);
}

void closeGate() {
  gateServo.write(0);
  digitalWrite(GREEN_LED, LOW);
  digitalWrite(RED_LED, HIGH);
}

void loop() {
  long distance = measureDistance();
  Serial.print("Distance: "); Serial.print(distance); Serial.println(" cm");

  if (distance > 0 && distance < DETECT_THRESHOLD_CM) {
    openGate();
    delay(GATE_OPEN_DELAY_MS);
    closeGate();
  }
  delay(100);
}
```

---

## 📸 Project Images

> 📷 *Hardware prototype images — add your own below*

| View | Description |
|---|---|
| ![Hardware Setup](https://via.placeholder.com/400x250?text=Hardware+Setup) | Full breadboard circuit with Arduino, sensor, and servo |
| ![Gate Open State](https://via.placeholder.com/400x250?text=Gate+Open+State) | Servo at 90° — Green LED active, vehicle detected |
| ![Gate Closed State](https://via.placeholder.com/400x250?text=Gate+Closed+State) | Servo at 0° — Red LED active, gate closed |

---

## 🎥 Demo / Preview

> 🔗 **[Watch the Live Demo on LinkedIn »](https://www.linkedin.com/)**

The demo showcases:
- Real-time vehicle detection with the ultrasonic sensor
- Servo gate actuation in response to proximity events
- LED indicator transitions between states
- Full auto-close behavior after gate open duration expires

---

## 📚 Learning Outcomes

By building this project, the following engineering skills were developed and reinforced:

- **Sensor Integration** — Interfacing and reading distance data from the HC-SR04 ultrasonic sensor
- **Actuator Control** — Driving a servo motor with precise angular control using PWM signals
- **Embedded C++ Programming** — Writing clean, structured Arduino sketches using functions and constants
- **Digital I/O Management** — Controlling LEDs and reading sensor states via GPIO pins
- **System Timing** — Implementing non-blocking-friendly delays and timed gate behavior
- **Hardware Prototyping** — Designing, wiring, and debugging a multi-component embedded circuit
- **Real-World Problem Solving** — Translating an infrastructure automation challenge into a working hardware solution

---

## 📈 Future Scope

This project can be significantly expanded with the following enhancements:

- [ ] **RFID / NFC Integration** — Identify registered vehicles and automate toll deduction
- [ ] **IoT Dashboard** — Send real-time vehicle counts and gate logs to a web dashboard via ESP8266/ESP32
- [ ] **LCD Display** — Show vehicle count, gate status, and balance info on-site
- [ ] **IR Sensor Redundancy** — Add secondary IR sensors for improved detection reliability
- [ ] **Camera Module** — Capture vehicle images at gate entry for logging and security
- [ ] **Mobile Alert System** — Push notifications to toll operators for anomalies or system faults
- [ ] **PCB Design** — Move from breadboard prototype to a custom-designed PCB for production use
- [ ] **Solar Power Integration** — Make the system energy-independent for rural deployment

---

## 📬 Connect

<div align="center">

If you found this project useful, insightful, or inspiring — let's connect!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/)
[![Email](https://img.shields.io/badge/Email-Reach%20Out-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:your@email.com)

</div>

---

<div align="center">

**⭐ If this project helped you, consider giving it a star — it keeps the momentum going!**

*Built with curiosity, circuits, and a lot of `Serial.println()` debugging.*

[![Made with Arduino](https://img.shields.io/badge/Made%20with-Arduino-00979D?style=flat-square&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Open Source](https://img.shields.io/badge/Open%20Source-Yes-brightgreen?style=flat-square)](https://github.com/)

</div>
