# 🗑️ SmartWaste Management System

### ESP32 • Embedded Systems • IoT • Sensor Interfacing • Cloud Monitoring

> An industry-oriented student prototype for intelligent waste monitoring using ESP32, ultrasonic sensing, automated lid control, local alerts, OLED visualization, and ThingSpeak cloud monitoring.

<p align="center">

![ESP32](https://img.shields.io/badge/ESP32-Embedded%20Controller-000000?style=for-the-badge&logo=espressif)
![C++](https://img.shields.io/badge/C%2FC%2B%2B-Firmware-00599C?style=for-the-badge&logo=cplusplus)
![IoT](https://img.shields.io/badge/IoT-Connected%20System-0A84FF?style=for-the-badge)
![Wokwi](https://img.shields.io/badge/Wokwi-Simulation-8B5CF6?style=for-the-badge)
![ThingSpeak](https://img.shields.io/badge/ThingSpeak-Cloud%20Monitoring-FF6B35?style=for-the-badge)

</p>

---

## ⚡ What is this?

**SmartWaste** is an ESP32-based IoT prototype designed to make waste-bin monitoring more intelligent and less dependent on manual inspection.

The system combines **physical sensing, embedded decision-making, actuator control, local feedback, and cloud monitoring** into one complete workflow.

Two ultrasonic sensors are used:

- 📏 One for **waste-level measurement**
- ✋ One for **hand detection**

The ESP32 processes the sensor data and controls:

- ⚙️ Automatic servo-operated lid
- 📺 OLED status display
- 🟢 Green status LED
- 🔴 Red alert LED
- 🔊 Buzzer

The processed data is also transmitted through Wi-Fi to **ThingSpeak** for remote monitoring and historical visualization.

---

# 🎯 Why this project?

Traditional dustbins provide no information about their current state.

A person generally needs to physically inspect the bin to determine:

> "Is it empty, partially filled, or ready for collection?"

This project demonstrates a small-scale IoT architecture where the bin can:

**Sense → Process → Decide → Act → Report**

That workflow is the core idea behind many modern embedded and IoT systems.

---

# 🧠 System at a Glance

```text
                     SMARTWASTE
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
       Hand Detection         Waste Detection
        HC-SR04 #1             HC-SR04 #2
              │                     │
              └──────────┬──────────┘
                         ▼
                    ┌─────────┐
                    │  ESP32  │
                    │ Firmware│
                    └────┬────┘
                         │
             ┌───────────┼────────────┐
             │           │            │
             ▼           ▼            ▼
          Servo        OLED       LED/Buzzer
          Control     Display       Alerts
             │
             ▼
        Automatic Lid
                         │
                         ▼
                      Wi-Fi
                         │
                         ▼
                  ┌────────────┐
                  │ ThingSpeak │
                  │   Cloud    │
                  └─────┬──────┘
                        │
                        ▼
                 IoT Dashboard
