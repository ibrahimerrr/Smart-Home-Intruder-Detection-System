# Smart-Home-Intruder-Detection-System

## Project Summary
This project is an IoT-based home security system designed to monitor residential entry points and detect potential intruders. The system utilizes an ESP32 microcontroller to process real-time data from a PIR motion sensor and an HC-SR04 ultrasonic distance sensor. Local feedback is provided via an OLED display, an active buzzer for auditory alerts, and an RGB LED for visual status indication. The entire system is integrated with Arduino IoT Cloud, allowing users to monitor sensor data, switch between AUTO and MANUAL security modes, and control the alarm system remotely from anywhere via a web or mobile dashboard.

## Components List
* **Microcontroller:** ESP32 Development Board
* **Sensor 1:** HC-SR501 PIR Motion Sensor
* **Sensor 2:** HC-SR04 Ultrasonic Distance Sensor
* **Display:** OLED Display
* **Actuator 1:** Active Buzzer
* **Actuator 2:** RGB LED
* **Misc:** Breadboard, External Power Supply Module, Servo Motor

* ## 🔌 Wiring Table (GPIO ↔ Pins)

| Component | Component Pin | ESP32 GPIO Pin | Notes |
| :--- | :--- | :--- | :--- |
| **PIR Sensor** | OUT / DATA | GPIO 19
| **Ultrasonic** | TRIG | GPIO 5 | |
| **Ultrasonic** | ECHO | GPIO 18 | |
| **OLED Display** | SDA | GPIO 21 | I2C Data |
| **OLED Display** | SCL | GPIO 22 | I2C Clock |
| **Buzzer** | + (Positive) | GPIO 23 | |
| **RGB LED** | R (Red) | GPIO 25 |
| **RGB LED** | G (Green) | GPIO 26 |
| **RGB LED** | B (Blue) | GPIO 27 |

<img width="1236" height="967" alt="Untitled Sketch 4_şema" src="https://github.com/user-attachments/assets/a375d272-696d-4611-a3e9-e90588257688" />

## Cloud Setup (Arduino IoT Cloud)
**Platform:** Arduino IoT Cloud

**Variables / Feeds:**
1. `distance` (Integer) - Read Only.
2. `motion_status` (Boolean) - Read Only.
3. `system_mode` (Boolean) - Read & Write, Update on Change.
4. `alarm_trigger` (Boolean) - Read & Write, Update on Change.
5. `rgb` (CloudColoredLight) - Read Only.
6. `System Status`(String) - Read & Write.

**Dashboard Widgets:**
* **Distance:** Gauge Widget
* **Motion Detection:** LED Widget
* **System Mode Switch (AUTO/MANUAL):** Switch Widget
* **Alarm:** Switch Widget
* **System Status :** Character String Widget
* **Status RGB:** Colored Light Widget

## How to Run
1. **Board Settings:** Install ESP32 board manager in Arduino IDE. Select your specific ESP32 board (e.g., "DOIT ESP32 DEVKIT V1").
2. **Required Libraries:** 
   * `Adafruit GFX Library`
   * `Adafruit SH110X` (for the OLED Display)
   * `WiFi Library`
   * `ArduinoIoTCloud` and `Arduino_ConnectionHandler` (Automatically included by web editor).
3. **Cloud Configuration:** Set up the Thing properties in Arduino Cloud and enter your Wi-Fi SSID and Password in the "Secret" tab.
4. Upload the code to the ESP32.

## How it Works
The system operates in two main modes controlled via the cloud dashboard:
* **AUTO Mode:** The system autonomously monitors the environment. If the PIR detects motion or the Ultrasonic sensor detects a distance drop (below the threshold, indicating an open door/window), the ESP32 triggers the local alarm (Buzzer = ON, LED = RED) and updates the cloud dashboard status light to Red. When safe, the LED remains Green.
* **MANUAL Mode:** The system ignores physical sensor thresholds. The alarm is strictly controlled by the user via the `alarm_trigger` button on the dashboard. The local RGB LED and Cloud Light turn Blue to indicate manual override mode.

**Safe Mode
<img width="1919" height="765" alt="dashboard auto" src="https://github.com/user-attachments/assets/953c271b-dab8-4288-8a39-0556d97d5ac6" />

**Intruder Detected
<img width="1919" height="730" alt="dashboard red auto" src="https://github.com/user-attachments/assets/99eaa61e-6dcf-4399-b03d-9536e0534ade" />

**Manuel Mode
<img width="1919" height="801" alt="dashboard manual" src="https://github.com/user-attachments/assets/f5042e98-e50f-49a5-a3d5-cfc02c51391d" />

**Notification Push: 

A notification will be pushed via Arduino Cloud IoT Remote App if alarm triggered and motion detected.
<img width="1080" height="1249" alt="aa" src="https://github.com/user-attachments/assets/9369e7e9-93c2-45d5-a5bd-e7a60ea3384c" />

