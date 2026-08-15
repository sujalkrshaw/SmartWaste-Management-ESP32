# Wokwi Simulation Notes

## Project

Smart Dustbin – ESP32 IoT-Based Smart Waste Management System

## Simulation Platform

Wokwi ESP32 Simulation

## Tested Components

- ESP32
- HC-SR04 – Hand Detection
- HC-SR04 – Waste-Level Detection
- Servo Motor
- OLED Display
- Green LED
- Red LED
- Buzzer
- Wi-Fi
- ThingSpeak Cloud

## Sensor Logic

### Hand Detection

When the hand distance is less than or equal to 10 cm:

- Lid opens
- Servo moves to approximately 90°
- Lid Status becomes OPEN

When the hand moves away:

- Lid closes
- Servo returns to approximately 0°
- Lid Status becomes CLOSED

### Waste-Level Detection

The simulated bin height is 20 cm.

Fill percentage:

Fill % = ((20 - Waste Distance) / 20) × 100

The value is limited between 0% and 100%.

### Full Bin Detection

Full threshold:

80%

When fill level reaches 80% or above:

- Bin Status = FULL / ALERT
- Red LED turns ON
- Buzzer turns ON

When fill level is below 80%:

- Bin Status = NORMAL
- Green LED turns ON
- Buzzer turns OFF

## IoT Communication

ESP32 connects to the Wokwi Wi-Fi network and sends sensor data to ThingSpeak.

### ThingSpeak Fields

| Field | Data |
|---|---|
| Field 1 | Fill Percentage |
| Field 2 | Waste Distance |
| Field 3 | Bin Status |
| Field 4 | Lid Status |
| Field 5 | Hand Distance |
| Field 6 | Bin ID |
| Field 7 | Connectivity |

## Test Results

### Test 1 – Wi-Fi

Result: PASS

ESP32 successfully connected to Wokwi-GUEST.

### Test 2 – Automatic Lid

Hand distance approximately 2 cm:

Result: PASS

Lid Status changed to OPEN.

Hand distance approximately 63.5 cm:

Result: PASS

Lid Status changed to CLOSED.

### Test 3 – Full Bin

Waste distance approximately 2 cm:

Fill level: approximately 90.1%

Bin Status: FULL / ALERT

Result: PASS

### Test 4 – ThingSpeak

ESP32 successfully transmitted data to ThingSpeak.

HTTP response:

200

Result: PASS

## Conclusion

The Wokwi simulation successfully demonstrates automatic lid control, waste-level monitoring, full-bin detection, local alerts, OLED monitoring, Wi-Fi connectivity and cloud-based ThingSpeak monitoring.