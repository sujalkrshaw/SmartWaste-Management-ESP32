# Smart Dustbin – System Architecture

## 1. Overview

The Smart Dustbin is an ESP32-based IoT system designed to monitor waste level and automate dustbin operation.

The system combines sensors, actuators, local display, alerts, Wi-Fi connectivity and cloud monitoring.

---

## 2. System Architecture

```text
                 ┌─────────────────────┐
                 │      HC-SR04        │
                 │  Hand Detection     │
                 └──────────┬──────────┘
                            │
                            ▼
                    ┌───────────────┐
                    │               │
                    │     ESP32     │
                    │               │
                    └───────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
        ┌─────────┐    ┌─────────┐    ┌─────────┐
        │  Servo  │    │  OLED   │    │  Alerts │
        │   Lid   │    │ Display │    │LED/Buzz │
        └─────────┘    └─────────┘    └─────────┘
                            │
                            │ Wi-Fi
                            ▼
                     ┌──────────────┐
                     │  ThingSpeak  │
                     │     Cloud     │
                     └──────┬───────┘
                            │
                            ▼
                     ┌──────────────┐
                     │ IoT Dashboard│
                     └──────────────┘

                 ┌─────────────────────┐
                 │      HC-SR04        │
                 │  Waste Detection    │
                 └──────────┬──────────┘
                            │
                            └──────────► ESP32