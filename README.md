# Driver Safety Dashboard 🌐📊  

This repository contains the web application for the **Anti-Sleep Glasses** project.  
The dashboard presents data collected from the glasses in a clean and interactive interface.  

### Features:
- Real-time driver alert status  
- Drowsiness event tracking & analytics  
- Trip summaries and history reports  
- Data visualizations (charts, graphs, maps)  
- Exportable insights for driver safety  

💻 Built to support the hardware component of the project by providing **data-driven insights** and **improving user experience**.

# 💤 AI-Powered Anti-Sleep Glasses  
*A Real-Time Drowsiness Detection System using ESP32, IMU Sensors, and Machine Learning*

---

## 🧩 Overview

The **AI-Powered Anti-Sleep Glasses** project integrates embedded systems, IoT, and machine learning to detect driver drowsiness based on **head motion and eye-blink activity**.  
It consists of an **ESP32 firmware layer**, **Python-based ML pipeline**, **Flask API server**, and a **Bootstrap-powered dashboard** for real-time visualization.

---

## ⚙️ Hardware (Edge Device)

| Component | Description | Role |
|------------|--------------|------|
| **ESP32 Dev Module** | Wi-Fi + Bluetooth SoC | Microcontroller; handles wireless comms and runs firmware in C++ (PlatformIO/Arduino). |
| **MPU6050 (Accelerometer + Gyroscope)** | 6-axis IMU sensor | Collects head motion data (nod detection). |
| **Li-Po Battery (3.7V, 1100–2200mAh)** | Flat pack battery | Portable power source. |
| **LEDs + Resistors (220Ω)** | Indicators | Visual alerts. |
| **Active Buzzer Module** | Audio module | Audible alert for drowsiness. |
| **Push Button Switch** | Input module | Resets alerts or toggles system on/off. |
| **IR + Photodiode Sensor** | Eye detection module | Detects blinks (second stage confirmation). |

---

## 💻 Firmware (on ESP32)

| Category | Details |
|-----------|----------|
| **Language** | C++ (Arduino framework via PlatformIO) |
| **Libraries** | `Wire.h` (I²C comms with MPU6050) • `Adafruit_MPU6050` (sensor driver) • `Adafruit_Sensor` (standard interface) • `Arduino.h` (core functions) |
| **IDE** | PlatformIO (VS Code Extension) |
| **Debugging** | Serial Monitor via PlatformIO |
| **Output** | Streams IMU and IR sensor data over Serial/Wi-Fi |

> The firmware continuously reads motion data, packages it as CSV-formatted logs, and streams to the connected host or server for processing.

---

## 📊 Data Logging & Machine Learning

### 🧠 Data Flow
- ESP32 firmware streams **IMU sensor data** over **Serial/Wi-Fi**.
- Data stored as `.csv` files in the `/data/` directory for analysis and ML training.

### 🧰 Tools / Frameworks
- **Python 3.10+**
- **Jupyter Notebook (Anaconda)** — for ML experimentation and visualization.

### 🧮 Libraries
| Library | Function |
|----------|-----------|
| **pandas** | Handle CSV logs |
| **numpy** | Numerical operations |
| **matplotlib / seaborn** | Visualization |
| **scikit-learn** | Model training & evaluation |
| **joblib** | Save trained models as `.pkl` |
| **StandardScaler** | Data normalization |

### 🧩 Models Used
- **Logistic Regression**
- **Random Forest Classifier**

### 🧾 ML Output Files
| File | Description |
|------|--------------|
| `scaler.pkl` | Preprocessing (StandardScaler) |
| `nod_rf.pkl` | Trained Random Forest model |
| `nod_lr.pkl` | Trained Logistic Regression model |

---

## 🌐 Server / API Layer

| Component | Description |
|------------|--------------|
| **Language** | Python |
| **Framework** | Flask + Flask-SocketIO |
| **Purpose** | Handle data streaming from ESP32, run ML inference, and broadcast live predictions to the dashboard. |

### 🧠 API Role
- Receives IMU/IR data from ESP32 (Wi-Fi or Serial)
- Loads ML model (`joblib`)
- Performs inference (Awake / Drowsy)
- Streams real-time classification results via WebSockets

### ⚙️ Dependencies
```bash
flask
flask-socketio
eventlet  # or gevent for async comms
joblib
pandas


