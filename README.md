# 🗑️ Smart Dustbin Embedded System

> **An ESP32-based embedded IoT system that combines contactless lid automation, waste-level monitoring, real-time alerts, and cloud-based telemetry into a practical smart-waste solution.**

<p align="center">
  <img src="https://img.shields.io/badge/ESP32-Embedded%20System-E7352C?style=for-the-badge&logo=espressif&logoColor=white" alt="ESP32">
  <img src="https://img.shields.io/badge/C%2FC%2B%2B-Firmware-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++">
  <img src="https://img.shields.io/badge/IoT-ThingSpeak-0B6EBD?style=for-the-badge" alt="ThingSpeak">
  <img src="https://img.shields.io/badge/Simulation-Wokwi-7B61FF?style=for-the-badge" alt="Wokwi">
</p>

<p align="center">
  <strong>Sense • Process • Decide • Actuate • Display • Communicate</strong>
</p>

---

## 📖 Overview

**Smart Dustbin Embedded System** is an ESP32-based embedded and IoT project developed to automate waste-bin interaction and monitor waste levels. The system uses ultrasonic sensors for two independent tasks: detecting a nearby hand for contactless lid operation and measuring the distance to the waste surface. The ESP32 processes these measurements and controls a servo motor, OLED display, LEDs, and buzzer according to the current system state. It also provides IoT connectivity through Wi-Fi and ThingSpeak for remote monitoring. The repository contains the firmware, circuit design, architecture documentation, Wokwi simulation resources, testing evidence, screenshots, and project report, making it a complete engineering portfolio project rather than only a hardware demonstration.

---

## ✨ Features

- ✋ Contactless hand detection for hygienic, hands-free operation  
- ⚙️ Automatic servo-controlled lid with independent open and close logic  
- 📏 Ultrasonic waste-distance measurement for bin-level estimation  
- 📊 Automatic conversion of measured distance into a fill percentage  
- 🚨 Threshold-based full-bin detection with visual and audible alerts  
- 📺 OLED interface for local real-time system information  
- 🟢 Green LED indication for normal operating conditions  
- 🔴 Red LED indication for full-bin conditions  
- 🔊 Buzzer notification when the configured full threshold is reached  
- 📡 ESP32 Wi-Fi connectivity for IoT communication  
- ☁️ ThingSpeak integration for remote telemetry and monitoring  
- 🧪 Wokwi simulation resources for development and validation  
- 📸 Dedicated project-proof section with real repository screenshots  
- 📚 Structured engineering documentation covering architecture, pins, simulation, and testing  

---

## 🗂️ Repository Structure

```text
SMART-DUSTBIN-EMBEDDED-SYSTEM/
│
├── arduino_code/
│   └── smart_dustbin.ino
│       └── Main ESP32 firmware
│
├── circuit_diagram/
│   └── circuit.png
│       └── Complete circuit diagram
│
├── docs/
│   ├── architecture.md
│   │   └── System architecture and design documentation
│   └── pin-configuration.md
│       └── ESP32 GPIO and hardware mapping
│
├── reports/
│   └── project-report.pdf
│       └── Formal project report
│
├── screenshots/
│   ├── BIN FULL.png
│   │   └── Full-bin operating state
│   ├── dashboard_pic1.png
│   │   └── ThingSpeak dashboard evidence
│   ├── dashboard_pic2.png
│   │   └── Additional dashboard evidence
│   ├── FULL+HAND DETECTION.png
│   │   └── Full-bin state with hand detection
│   ├── HAND DETECTION.png
│   │   └── Hand detection test evidence
│   ├── HAND REMOVAL.png
│   │   └── Hand removal test evidence
│   └── NORMAL BIN.png
│       └── Normal operating state
│
├── simulation/
│   ├── diagram.json
│   │   └── Wokwi simulation configuration
│   ├── libraries.txt
│   │   └── Simulation library dependencies
│   └── simulation_notes.md
│       └── Simulation documentation
│
├── .gitignore
│   └── Git version-control exclusions
│
└── README.md
    └── Project documentation
````

---

## 🚀 How It Works

The system follows an embedded control pipeline:

```text
              USER / WASTE
                   │
                   ▼
            ┌─────────────┐
            │   SENSORS   │
            └──────┬──────┘
                   │
                   ▼
             ┌───────────┐
             │   ESP32   │
             │           │
             │ Read      │
             │ Process   │
             │ Decide    │
             └─────┬─────┘
                   │
        ┌──────────┼──────────┐
        │          │          │
        ▼          ▼          ▼
      SERVO       OLED     LED/BUZZER
        │          │          │
        └──────────┼──────────┘
                   │
                   ▼
                 Wi-Fi
                   │
                   ▼
              ThingSpeak
                   │
                   ▼
           Remote Monitoring
```

### 1. Hand Detection

The first ultrasonic sensor monitors the area in front of the dustbin.

```text
Hand distance ≤ configured threshold
                ↓
          Hand detected
                ↓
        Servo opens the lid
```

When the hand moves away:

```text
Hand distance > configured threshold
                ↓
         No hand detected
                ↓
        Servo closes the lid
```

### 2. Waste-Level Monitoring

The second ultrasonic sensor measures the distance from the sensor to the waste surface.

The project uses the measured distance to estimate the percentage of available bin capacity that has been occupied.

```text
Fill % = ((Bin Height - Waste Distance) / Bin Height) × 100
```

The calculated value is constrained to a valid 0–100% range.

### 3. Bin-State Decision

The firmware evaluates the calculated fill level against the configured full-bin threshold.

```text
                    Fill Level
                        │
             ┌──────────┴──────────┐
             │                     │
          Normal                 Full
             │                     │
             ▼                     ▼
       Green LED ON          Red LED ON
       Buzzer OFF             Buzzer ON
```

### 4. Local Feedback

The OLED provides local system information while the LEDs and buzzer provide immediate state feedback.

### 5. IoT Monitoring

The ESP32 uses Wi-Fi to communicate with ThingSpeak, allowing system measurements and states to be monitored remotely.

---

## 📦 Technologies Used

**Microcontroller:** ESP32

**Programming:** C/C++, Arduino Framework

**Sensors:** HC-SR04 Ultrasonic Sensors

**Actuation:** Servo Motor

**Display:** SSD1306 OLED

**Indicators:** Green LED, Red LED, Buzzer

**Communication:** Wi-Fi, HTTP, I²C

**Cloud Platform:** ThingSpeak

**Simulation:** Wokwi

**Development:** Arduino IDE, Git, GitHub

---

## 🔧 Configuration Options

The project keeps hardware and system configuration within the firmware and supporting documentation.

| Configuration            | Purpose                                        |
| ------------------------ | ---------------------------------------------- |
| Hand detection threshold | Determines when the lid should open            |
| Bin height               | Reference dimension for fill-level calculation |
| Full-bin threshold       | Determines when the bin enters alert mode      |
| Servo open position      | Controls the lid-open position                 |
| Servo closed position    | Controls the lid-closed position               |
| Wi-Fi credentials        | Provides network connectivity                  |
| ThingSpeak configuration | Enables cloud telemetry                        |

### ESP32 Pin Configuration

| Component     | Function |      GPIO |
| ------------- | -------- | --------: |
| Hand HC-SR04  | TRIG     |    GPIO 5 |
| Hand HC-SR04  | ECHO     |   GPIO 18 |
| Waste HC-SR04 | TRIG     |   GPIO 19 |
| Waste HC-SR04 | ECHO     |   GPIO 23 |
| Servo Motor   | Signal   |   GPIO 13 |
| Green LED     | Control  |   GPIO 25 |
| Red LED       | Control  |   GPIO 26 |
| Buzzer        | Control  |   GPIO 27 |
| OLED          | I²C      | SDA / SCL |

Detailed mapping is also available in [`docs/pin-configuration.md`](docs/pin-configuration.md).

### Credential Security

Private credentials such as Wi-Fi passwords and ThingSpeak API keys should not be committed to a public repository.

Use configuration placeholders rather than exposing real credentials.

---

## 📊 Outputs

* `OLED Display` – local display of system measurements and operating state
* `Servo Motor` – physical automatic lid movement
* `Green LED` – normal-bin indication
* `Red LED` – full-bin indication
* `Buzzer` – audible full-bin alert
* `Serial Monitor` – firmware and sensor diagnostics
* `ThingSpeak` – remote IoT telemetry and visualization
* `screenshots/` – visual evidence of tested operating conditions
* `reports/project-report.pdf` – detailed project documentation

### ThingSpeak Data

The project uses structured telemetry for cloud monitoring:

| Field   | Data            |
| ------- | --------------- |
| Field 1 | Fill Percentage |
| Field 2 | Waste Distance  |
| Field 3 | Bin Status      |
| Field 4 | Lid Status      |
| Field 5 | Hand Distance   |
| Field 6 | Bin ID          |
| Field 7 | Connectivity    |

---

# 🔬 Project Proof & Screenshots

> **The images below are kept exclusively in the project-proof section to provide visual evidence of the implemented system and tested states.**

## ⚡ Circuit Implementation

<p align="center">
  <img src="circuit_diagram/circuit.png" alt="Smart Dustbin Circuit Diagram" width="900">
</p>

**Circuit diagram:** [`circuit_diagram/circuit.png`](circuit_diagram/circuit.png)

---

## 🟢 Normal Bin State

<p align="center">
  <img src="screenshots/NORMAL%20BIN.png" alt="Normal Bin Test" width="850">
</p>

The normal-bin screenshot provides evidence of the system operating below the configured full-bin threshold.

---

## 🔴 Full Bin State

<p align="center">
  <img src="screenshots/BIN%20FULL.png" alt="Full Bin Test" width="850">
</p>

This test demonstrates the full-bin condition and the corresponding alert behavior.

---

## ✋ Hand Detection

<p align="center">
  <img src="screenshots/HAND%20DETECTION.png" alt="Hand Detection Test" width="850">
</p>

The hand-detection test demonstrates contactless user detection and the corresponding lid-control behavior.

---

## ↩️ Hand Removal

<p align="center">
  <img src="screenshots/HAND%20REMOVAL.png" alt="Hand Removal Test" width="850">
</p>

This test demonstrates the system response after the user moves away from the detection zone.

---

## 🚨 Full Bin + Hand Detection

<p align="center">
  <img src="screenshots/FULL%2BHAND%20DETECTION.png" alt="Full Bin and Hand Detection Test" width="850">
</p>

This combined test demonstrates that **waste-level state and user-detection state are handled independently**.

A bin can remain full while the lid responds separately to the presence or absence of a user.

---

## ☁️ IoT Dashboard Proof

<p align="center">
  <img src="screenshots/dashboard_pic1.png" alt="ThingSpeak Dashboard" width="850">
</p>

<p align="center">
  <img src="screenshots/dashboard_pic2.png" alt="ThingSpeak Dashboard Additional View" width="850">
</p>

These screenshots provide visual evidence of the cloud-monitoring side of the project.

---

## 🧪 Testing & Validation

The project includes dedicated screenshots and simulation resources to demonstrate functional behavior.

| Test Scenario        | Expected Behavior          | Evidence                                   |
| -------------------- | -------------------------- | ------------------------------------------ |
| Normal bin           | Normal indication          | `NORMAL BIN.png`                           |
| Full bin             | Full/alert indication      | `BIN FULL.png`                             |
| Hand detected        | Lid opens                  | `HAND DETECTION.png`                       |
| Hand removed         | Lid closes                 | `HAND REMOVAL.png`                         |
| Full + hand detected | Independent state handling | `FULL+HAND DETECTION.png`                  |
| Cloud monitoring     | Dashboard data available   | `dashboard_pic1.png`, `dashboard_pic2.png` |

### Validation Approach

```text
          Requirement
               │
               ▼
        Firmware Logic
               │
               ▼
          Simulation
               │
               ▼
       Functional Testing
               │
               ▼
       Screenshot Evidence
               │
               ▼
        Cloud Verification
```

---

## 🧪 Simulation

The repository includes a dedicated simulation environment:

```text
simulation/
├── diagram.json
├── libraries.txt
└── simulation_notes.md
```

The simulation resources support development and validation of the embedded control logic before or alongside physical hardware testing.

The simulation architecture covers:

* ESP32
* Ultrasonic sensors
* Servo motor
* OLED display
* LEDs
* Buzzer
* Wi-Fi communication
* IoT monitoring behavior

---

## 🧠 Engineering Concepts Demonstrated

### Embedded Firmware

* ESP32 programming
* C/C++ firmware development
* GPIO configuration
* Sensor acquisition
* Distance measurement
* Threshold-based decision logic
* Servo control
* Peripheral integration
* Serial debugging

### Electronics

* Ultrasonic sensor interfacing
* Servo integration
* OLED/I²C communication
* LED indicators
* Buzzer control
* Microcontroller-based circuit design

### IoT

* Wi-Fi connectivity
* HTTP communication
* Cloud telemetry
* ThingSpeak integration
* Remote monitoring

### Engineering Workflow

```text
Problem
   ↓
Requirements
   ↓
Architecture
   ↓
Circuit Design
   ↓
Firmware
   ↓
Simulation
   ↓
Testing
   ↓
Cloud Integration
   ↓
Documentation
```

---

## 📐 Architecture Documentation

The project includes dedicated documentation for engineering reference:

* [`docs/architecture.md`](docs/architecture.md) – system architecture
* [`docs/pin-configuration.md`](docs/pin-configuration.md) – hardware/GPIO mapping
* [`simulation/simulation_notes.md`](simulation/simulation_notes.md) – simulation documentation
* [`reports/project-report.pdf`](reports/project-report.pdf) – formal project report

The separation of firmware, hardware documentation, simulation, testing evidence, and reports makes the repository easier to understand and extend.

---

## 🤝 Contributing

The existing architecture provides several practical directions for improvement.

* Improve ultrasonic measurement stability using filtering and calibration
* Add configurable thresholds and operating parameters
* Implement sensor-failure detection and recovery
* Add automatic Wi-Fi reconnection handling
* Improve reliability of cloud data transmission
* Add remote notifications when the bin reaches capacity
* Extend the firmware to support multiple smart bins
* Add device identification and location tracking
* Build a dedicated web or mobile monitoring interface
* Add historical fill-rate analytics
* Investigate MQTT for scalable IoT deployments
* Optimize power consumption for battery-powered operation

---

## 📝 Known Limitations

* The current implementation represents a single smart-bin prototype.
* Waste level is estimated using ultrasonic distance measurement.
* The current decision model is threshold-based.
* Cloud monitoring depends on Wi-Fi availability.
* Simulation cannot reproduce every physical-world condition.
* Physical deployment requires additional electrical, mechanical, and environmental validation.
* Long-duration reliability testing is not part of the current repository.
* Multi-bin fleet management is not currently implemented.
* Predictive waste-generation analysis is not currently implemented.
* Industrial deployment would require additional security, enclosure, power-management, and reliability engineering.

---

## ❤️ Acknowledgements

This project was developed as an **ECE-focused embedded systems and IoT project** with an emphasis on practical implementation and engineering documentation.

The work combines ESP32 firmware, ultrasonic sensing, servo actuation, OLED interfacing, local alert mechanisms, Wi-Fi communication, ThingSpeak monitoring, Wokwi simulation, and documented functional testing.

---

## 🔧 Things to Improve (Roadmap)

* [ ] Add sensor calibration and measurement filtering
* [ ] Add configurable firmware parameters
* [ ] Add sensor fault detection
* [ ] Add automatic Wi-Fi reconnection
* [ ] Add cloud communication retry handling
* [ ] Add remote notifications
* [ ] Build a dedicated web dashboard
* [ ] Develop a mobile monitoring interface
* [ ] Support multiple smart bins
* [ ] Add unique device identification
* [ ] Add bin location tracking
* [ ] Add historical waste-level analytics
* [ ] Explore predictive fill-level estimation
* [ ] Evaluate MQTT communication
* [ ] Improve credential and security management
* [ ] Optimize power consumption
* [ ] Build a complete physical enclosure
* [ ] Perform long-duration hardware validation

---

# 👨‍💻 Author

## **Sujal Kumar Shaw**

**ECE Student | Embedded Systems | IoT | Electronics**

### Technical Interests

`Embedded Systems` · `ESP32` · `Embedded C/C++` · `IoT` · `Firmware Development` · `Electronics` · `Sensor Interfacing` · `Automation`

I enjoy building practical engineering systems that connect **hardware, firmware, sensors, automation, and IoT** to solve real-world problems.

> **Build. Test. Document. Improve.**

---

## ⭐ Project Value

This project demonstrates an end-to-end engineering workflow rather than a standalone sensor experiment.

```text
                 HARDWARE
                    │
        ┌───────────┴───────────┐
        │                       │
     Sensors                 Actuator
        │                       │
        └───────────┬───────────┘
                    ▼
                  ESP32
                    │
                    ▼
                Firmware
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      OLED        Alerts       Servo
        │           │           │
        └───────────┼───────────┘
                    ▼
                  Wi-Fi
                    │
                    ▼
               ThingSpeak
                    │
                    ▼
             Cloud Monitoring
```

### What this project demonstrates

**Embedded Firmware**
ESP32 programming, C/C++, GPIO, sensor acquisition, control logic, and debugging.

**Hardware Integration**
Ultrasonic sensors, servo motor, OLED, LEDs, buzzer, and microcontroller interfacing.

**IoT Engineering**
Wi-Fi connectivity, HTTP communication, ThingSpeak telemetry, and remote monitoring.

**Engineering Practice**
Architecture design, simulation, functional testing, evidence collection, documentation, and version control.

---

## 📄 Project Resources

| Resource          | Link                                                               |
| ----------------- | ------------------------------------------------------------------ |
| Firmware          | [`arduino_code/smart_dustbin.ino`](arduino_code/smart_dustbin.ino) |
| Circuit           | [`circuit_diagram/circuit.png`](circuit_diagram/circuit.png)       |
| Architecture      | [`docs/architecture.md`](docs/architecture.md)                     |
| Pin Configuration | [`docs/pin-configuration.md`](docs/pin-configuration.md)           |
| Simulation        | [`simulation/diagram.json`](simulation/diagram.json)               |
| Simulation Notes  | [`simulation/simulation_notes.md`](simulation/simulation_notes.md) |
| Project Report    | [`reports/project-report.pdf`](reports/project-report.pdf)         |
| Screenshots       | [`screenshots/`](screenshots/)                                     |

---

## 🏁 Final Summary

```text
SENSE
  ↓
PROCESS
  ↓
DECIDE
  ↓
ACTUATE
  ↓
DISPLAY
  ↓
COMMUNICATE
  ↓
MONITOR
```

### 🗑️ Smart Dustbin Embedded System

**ESP32 • Embedded C/C++ • Sensors • Automation • IoT • ThingSpeak • Wokwi**

**Designed and developed by Sujal Kumar Shaw**

**ECE Student | Embedded Systems & IoT**

```
```
