# 🗑️ HYGIENIX – Smart Touchless Dustbin and Waste-Level Alert System Using Arduino

HYGIENIX is an Arduino-based smart dustbin prototype designed to provide **touchless lid operation** and **waste-level alerts**.

The system uses ultrasonic sensors to detect a nearby hand and monitor the waste level. A servo motor automatically opens and closes the dustbin lid, while an LED and buzzer provide visual and audible alerts when garbage reaches the predefined threshold.

---

## 🚀 Features

* ✋ **Touchless Lid Opening**

  * Detects a hand/object within **15 cm** using an ultrasonic sensor.
  * Automatically opens the lid to **90°**.

* 🔄 **Automatic Lid Closing**

  * Keeps the lid open for approximately **3 seconds**.
  * Automatically returns the lid to **0°**.

* 🗑️ **Waste-Level Detection**

  * A second ultrasonic sensor monitors the waste level.
  * A distance of **10 cm or less** triggers the waste-level alert.

* 💡 **LED Alert**

  * LED flashes when the waste reaches the predefined threshold.

* 🔊 **Buzzer Alert**

  * Buzzer connected to **Digital Pin 10** provides an audible warning when the dustbin reaches the threshold.

* 🖥️ **Serial Monitor**

  * Displays hand sensor distance, garbage sensor distance and system status at **9600 baud**.

---

## 🛠️ Components Required

| Component                            |    Quantity | Purpose                        |
| ------------------------------------ | ----------: | ------------------------------ |
| Arduino-compatible development board |           1 | Main controller                |
| HC-SR04 Ultrasonic Sensor            |           2 | Hand and waste-level detection |
| Servo Motor                          |           1 | Automatic lid movement         |
| LED                                  |           1 | Visual waste-level alert       |
| Resistor                             |           1 | LED current limiting           |
| Buzzer                               |           1 | Audible waste-level alert      |
| Breadboard                           |           1 | Circuit prototyping            |
| Jumper Wires                         | As required | Connections                    |
| USB Cable / Power Source             |           1 | Programming and power          |
| Dustbin with movable lid             |           1 | Mechanical structure           |

---

## 🔌 Circuit Connections

| Component           | Pin                    | Arduino Pin |
| ------------------- | ---------------------- | ----------- |
| Ultrasonic Sensor 1 | TRIG                   | D2          |
| Ultrasonic Sensor 1 | ECHO                   | D3          |
| Ultrasonic Sensor 2 | TRIG                   | D4          |
| Ultrasonic Sensor 2 | ECHO                   | D5          |
| LED                 | Anode through resistor | D6          |
| Servo Motor         | Signal                 | D9          |
| Buzzer              | Positive (+)           | D10         |
| All Components      | GND                    | GND         |

### Sensor Functions

**Ultrasonic Sensor 1 – Hand Detection**

* TRIG → D2
* ECHO → D3
* Detection threshold → **15 cm**

**Ultrasonic Sensor 2 – Waste-Level Detection**

* TRIG → D4
* ECHO → D5
* Waste threshold → **10 cm**

---

## ⚙️ Working Principle

The system operates in the following sequence:

```text
        Start
          │
          ▼
  Initialize Arduino
          │
          ▼
 Read Hand Distance
          │
          ▼
 Hand ≤ 15 cm?
      /       \
    Yes        No
     │          │
     ▼          │
 Open Lid       │
   90°          │
     │          │
     ▼          │
 Wait 3 sec     │
     │          │
     ▼          │
 Close Lid      │
     │          │
     └────┬─────┘
          ▼
 Read Waste Distance
          │
          ▼
 Waste ≤ 10 cm?
      /       \
    Yes        No
     │          │
     ▼          ▼
 LED + Buzzer   LED + Buzzer
     ON           OFF
     │
     ▼
   Repeat
```

---

## 💻 Software

The project is developed using:

* **Arduino IDE**
* **Arduino C/C++**
* **Servo.h Library**
* **Serial Monitor – 9600 Baud**

---

## 📂 Project Structure

```text
HYGIENIX/
│
├── HYGIENIX.ino
├── README.md
└── Project_Report/
    └── HYGIENIX_Project_Report.pdf
```

You can rename the `.ino` file according to your actual filename.

---

## 🧠 Programming Concepts Used

This project demonstrates several programming concepts:

* Variables
* Constants
* Functions
* Function parameters
* Conditional statements
* `if-else`
* `void setup()`
* `void loop()`
* Digital input/output
* Arithmetic calculations
* Serial communication
* Timing using `delay()`
* Ultrasonic distance calculation
* Servo motor control

---

## 📏 Distance Calculation

The ultrasonic sensor measures the time taken for the sound wave to return.

The program calculates distance using:

```text
Distance = Duration × 0.0343 / 2
```

If no echo is received within the timeout period, the program returns:

```text
999 cm
```

as a no-echo sentinel value.

---

## 🔔 Alert Conditions

| Condition          | Action                      |
| ------------------ | --------------------------- |
| Hand ≤ 15 cm       | Lid opens to 90°            |
| After 3 seconds    | Lid closes to 0°            |
| Garbage ≤ 10 cm    | LED flashes + buzzer sounds |
| Garbage > 10 cm    | LED and buzzer remain OFF   |
| No ultrasonic echo | Distance reported as 999 cm |

---

## 🧪 Expected Output

### Normal Condition

```text
Hand Sensor: 25 cm   Garbage Sensor: 18 cm
```

The lid remains closed and the alert devices remain OFF.

### Hand Detection

```text
Hand Sensor: 12 cm   Garbage Sensor: 18 cm
Hand detected! Opening lid...
Closing lid...
```

The servo opens the lid to 90° and closes it after approximately 3 seconds.

### Dustbin Full Alert

```text
Hand Sensor: 20 cm   Garbage Sensor: 8 cm
DUSTBIN FULL! BUZZER ON!
```

The LED flashes and the buzzer sounds.

---

## 🎯 Objectives

* Detect a user's hand without physical contact.
* Open the dustbin lid automatically using a servo motor.
* Close the lid automatically after a fixed three-second interval.
* Detect when garbage is close to the waste-level ultrasonic sensor.
* Provide visual and audible alerts using an LED and buzzer.
* Display sensor distances and system messages through the Serial Monitor.
* Demonstrate procedural programming concepts using an embedded system.

---

## 🌍 Applications

HYGIENIX can be adapted for:

* 🏠 Homes
* 🏫 Classrooms
* 🔬 Educational laboratories
* 🏢 Offices
* 🏥 Indoor areas
* 🚮 Smart waste-bin demonstrations

---

## 🔮 Future Scope

Possible future improvements include:

* OLED/LCD display for bin status
* Calibrated waste-level percentage measurement
* Improved buzzer alert patterns
* RGB status indicator
* Wi-Fi/Bluetooth connectivity
* Mobile or web dashboard
* Battery-powered operation
* Improved mechanical lid mechanism
* Sensor filtering and averaging
* Non-blocking `millis()`-based timing
* Dust- and moisture-protected enclosure

---

## ⚠️ Limitations

The current prototype uses simple distance thresholds.

* The ultrasonic sensor detects objects based on distance; it does not identify a human specifically.
* The **10 cm threshold is not a calibrated percentage of bin capacity**.
* Ultrasonic readings can vary depending on object shape, angle and surrounding conditions.
* The servo may require a suitable external power source depending on the motor used.
* The current program uses `delay()`, which temporarily blocks other operations.

---

## 👨‍💻 Project Team

**Visvaa S**
**Raghulram S**
**Toodi Raghul Reddy**

### Academic Year

**2026–2027**

### Project Type

**Mini Project – Procedural Programming**

---

## 📜 License

This project is created for **educational and academic purposes**.

You are welcome to study, modify and improve the project for learning purposes.

---

## ⭐ Acknowledgement

This project was developed as an Arduino-based academic prototype to demonstrate **touchless automation, ultrasonic sensing, servo control, LED indication and buzzer-based waste-level alerts**.
