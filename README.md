# 🌧️ Smart Rain Detector System

An Arduino Uno-based automated **Rain Detector System** developed as a **Digital Logic Design Lab (CSE-2324)** project at **International Islamic University Chittagong (IIUC)**. This system detects rainfall in real time and responds by activating an automatic cloth protection shield, triggering an audio-visual alarm, and turning on outdoor lighting for safety and visibility.

---

## 📂 Repository Contents

| File / Folder | Description |
| :--- | :--- |
| 📁 `circuit images/` | Contains circuit diagrams for the alarm, lighting control, cloth protection mechanism, and hardware prototype photos. |
| 📊 `Presentation on Rain Detector System.pptx` | Project presentation slides (**includes the simulation/demo video**). |
| 📄 `Report on Project Rain Detector System.pdf` | Complete project report covering methodology, circuit design, implementation, testing, and results. |
| 📝 `README.md` | Project overview, setup instructions, pin configuration, and source code. |

> **Note:** To view the **simulation video**, please download and open the PowerPoint presentation (`Presentation on Rain Detector System`) located in this repository.

---

## ✨ Key Features

1. **Automatic Cloth Protection:** Uses a rain sensor and a 9g servo motor to automatically deploy a protective cover over clothes or outdoor belongings when rain is detected, and retract it once the rain stops.
2. **Timely Rain Alerts (Alarm System):** Activates a buzzer and an LED immediately upon detecting rainfall, providing both audible and visual alerts.
3. **Intelligent Lighting Control:** Automatically switches on an LED light during rainy conditions to improve outdoor visibility and security.

---

## 🛠️ Hardware & Software Requirements

### Hardware Components
* **Arduino Uno** (Microcontroller)
* **Rain Sensor Module (YL-83)**
* **Servo Motor (Tower Pro SG90 9g)**
* **Buzzer**
* **LED** (with resistor as needed)
* **Breadboard**
* **Jumper Cables** (M-M, M-F, F-F)

### Software
* **Arduino IDE**

---

## 🔌 Pin Connections

| Component | Component Pin | Connected To |
| :--- | :--- | :--- |
| **Breadboard** | Positive (`+`) | Arduino `5V` |
| **Breadboard** | Negative (`-`) | Arduino `GND` |
| **Rain Sensor** | `VCC` | Breadboard `+` (`5V`) |
| **Rain Sensor** | `GND` | Breadboard `-` (`GND`) |
| **Rain Sensor** | `A0` (Analog Out) | Arduino `A3` |
| **Servo Motor (9g)** | Power (`+`) | Breadboard `+` (`5V`) |
| **Servo Motor (9g)** | Ground (`-`) | Breadboard `-` (`GND`) |
| **Servo Motor (9g)** | Control (Signal) | Arduino Digital Pin `5` |
| **LED** | Anode (`+`) | Arduino Digital Pin `4` |
| **LED** | Cathode (`-`) | Arduino `GND` |
| **Buzzer** | Positive (`+`) | LED (`+`) (Arduino Digital Pin `4`) |
| **Buzzer** | Negative (`-`) | LED (`-`) (`GND`) |

---

## 💻 Arduino Source Code

Upload the following sketch to your Arduino Uno using the Arduino IDE:

```cpp
#include <Servo.h>
Servo tap_servo;

void setup() {
  Serial.begin(9600);    // Enable serial monitor
  pinMode(4, OUTPUT);    // Define LED & Buzzer pin
  tap_servo.attach(5);   // Attach servo motor to pin 5
}

void loop() {
  int value = analogRead(A3); // Read analog value from rain sensor
  Serial.print("Value: ");
  Serial.println(value);

  if (value < 500) {
    tap_servo.write(-90);     // Rotate the servo motor to cover clothes
    Serial.println("Heavy rain.");
    digitalWrite(4, HIGH);    // Turn on LED and Buzzer
  } else {
    tap_servo.write(0);       // Rotate the servo motor back to 0 degrees
    Serial.println("No heavy rain - Servo motor at 0 degrees");
    digitalWrite(4, LOW);     // Turn off LED and Buzzer
  }
}
```

### How It Works
* The rain sensor continuously outputs an analog voltage to pin `A3`.
* When the sensor is dry, the analog reading stays at or above `500`, keeping the servo at `0°` and the LED/buzzer `LOW`.
* When raindrops fall on the YL-83 sensing pad, the conductivity increases and the analog value drops below `500`.
* Once the value drops below `500`, the Arduino drives the servo motor to protect the clothes and sets Digital Pin `4` to `HIGH`, turning on the LED and sounding the buzzer.

---

## 🚀 Future Improvements

* Integration with real-time weather APIs for predictive actions.
* Mobile/web dashboard for remote monitoring (IoT integration).
* Adding temperature and humidity sensors (e.g., DHT11/DHT22) for richer environmental monitoring.
* Power optimization for battery/solar-powered outdoor deployment.

---

## 👥 Project Team & Course Details

* **Course Title:** Digital Logic Design Lab
* **Course Code:** CSE-2324
* **Department:** Computer Science and Engineering (CSE)
* **Institution:** International Islamic University Chittagong (IIUC)
* **Submission Date:** 04 November 2023

### Submitted To
* **MD. Ziaur Rahman** — Lecturer, Dept. of CSE, International Islamic University Chittagong

### Submitted By (Section: 3AF | Semester: 3rd)
| Name | Student ID |
| :--- | :--- |
| **Akhi Moon Jahan** | `C223202` |
| **Syeda Afra Anam** | `C223205` |
| **Jarin Islam Shova** | `C223217` |

---

## 📚 References

* [Arduino Project Hub](https://projecthub.arduino.cc/)
* [Arduino IDE Software](https://www.arduino.cc/en/software)
* [Arduino Uno Rev3 Documentation](https://docs.arduino.cc/hardware/uno-rev3)
* [Rain Sensor Guide - WatElectronics](https://www.watelectronics.com/rain-sensor/)
* [Servo Motor Basics - Circuit Digest](https://circuitdigest.com/article/servo-motor-working-and-basics)
* [Buzzer Working & Applications - ElProCus](https://www.elprocus.com/buzzer-working-applications/)
