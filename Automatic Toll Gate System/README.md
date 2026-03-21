# 🚦 Automatic Toll Gate System

An Arduino-based **Automatic Toll Gate System** that detects vehicles using an ultrasonic sensor and automatically opens/closes the gate using a servo motor with LED status indicators.

---

## 🧾 Tech Stack

![Arduino](https://img.shields.io/badge/Arduino-Uno-00979D?style=for-the-badge&logo=arduino)
![Language](https://img.shields.io/badge/Language-C++-00599C?style=for-the-badge&logo=c%2B%2B)
![Sensor](https://img.shields.io/badge/Sensor-HC--SR04-blue?style=for-the-badge)
![Actuator](https://img.shields.io/badge/Actuator-Servo-orange?style=for-the-badge)
![Indicators](https://img.shields.io/badge/Indicators-LED%20Status-green?style=for-the-badge)

---

## 📍 Project Overview

This Automatic Toll Gate System is a smart embedded prototype designed to automate toll gate operation.

The system:

✔ Detects vehicles using an ultrasonic sensor  
✔ Opens the gate automatically using a servo motor  
✔ Uses LED indicators to show gate status  
✔ Closes the gate after a delay  

This is a low-cost academic prototype demonstrating transportation automation concepts.

⚠️ Educational project (not a commercial toll system).

---

## 🎥 Project Demo

📹 Watch the working demo on LinkedIn:  
👉 https://www.linkedin.com/posts/roshan-gupta-rg7755_embeddedsystems-arduino-automation-ugcPost-7441113272117874688-mzUh

---

## 🧰 Components Used

| Component | Quantity |
|-----------|----------|
| Arduino UNO | 1 |
| Ultrasonic Sensor (HC-SR04) | 1 |
| Servo Motor (SG90) | 1 |
| Red LED | 1 |
| Green LED | 1 |
| Resistors (220Ω) | 2 |
| Breadboard | 1 |
| Jumper Wires | As required |

---

## 🔌 Pin Configuration

| Device | Arduino Pin |
|--------|------------|
| Ultrasonic TRIG | 10 |
| Ultrasonic ECHO | 11 |
| Servo Motor | 9 |
| Green LED | 6 |
| Red LED | 7 |
| VCC | 5V |
| GND | GND |

---

## ⚙️ Working Principle

1. Ultrasonic sensor continuously measures distance.  
2. When a vehicle is detected:  
   - 🟢 Green LED ON (Gate Open)  
   - 🔴 Red LED OFF  
   - Servo opens gate  
3. After delay:  
   - 🔴 Red LED ON (Gate Closed)  
   - 🟢 Green LED OFF  
   - Servo closes gate  

---

## 💻 Arduino Logic

```
If (distance < threshold)
{
   Open Gate
   Green LED ON
   Red LED OFF
}
Else
{
   Close Gate
   Red LED ON
   Green LED OFF
}
```

---

## 📂 Project Structure

```
Automatic Toll Gate System/
│
├── automatic_toll_gate_system.ino
├── circuit-diagram.png
├── setup-image.jpg
└── README.md
```

---

## 🚀 Key Features

✔ Automatic vehicle detection  
✔ Servo-controlled gate mechanism  
✔ LED-based status indication  
✔ Simple and low-cost design  
✔ Expandable for RFID or IoT  

---

## 🔮 Future Enhancements

- RFID Integration  
- IoT Monitoring  
- Payment System  
- Smart Toll Analytics  

---

## 👨‍💻 Developed By

**Roshan Gupta**  
Embedded-Innovation-Lab  
BCA Student  

---

## 🔗 Professional Network

LinkedIn:  
https://www.linkedin.com/in/roshan-gupta-rg7755

---

## ⭐ Support

⭐ Star the repository  
🍴 Fork it  
🔗 Share on LinkedIn  

---

## 📜 License

Open-source for educational and innovation purposes.
