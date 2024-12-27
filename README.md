# Weather Control and Air Conditioning System  

## Project Overview  
The Weather Control and Air Conditioning System is an IoT-based solution that allows users to monitor and control indoor environments remotely. The app interfaces with embedded hardware (ESP32) and provides real-time data visualization, device control, scheduling, and automation.  

---

## Features  
- **Real-time Monitoring** – View temperature, humidity, and air quality.  
- **Device Control** – Adjust air conditioning, heating, and ventilation remotely.  
- **Scheduling** – Set automated schedules for HVAC systems.  
- **AI Automation** – Adaptive controls based on weather patterns and past usage.  
- **Energy Tracking** – Analyze energy consumption and receive savings recommendations.  
- **Alerts and Notifications** – Receive warnings for abnormal conditions.  
- **Multi-Zone Management** – Control different rooms and zones individually.  
- **Smart Home Integration** – Connect with Google Home, Alexa, and Apple HomeKit.  

---

## Technologies  
- **Frontend**: Flutter (iOS, Android, Web)  
- **Backend**: Django (Python), Firebase (optional)  
- **Communication**: MQTT, WebSockets, REST APIs  
- **Embedded System**: ESP32 (C++)  
- **Deployment**: Docker, Nginx, Gunicorn  

---

## Wireframe and UI Design  
### 1. Dashboard (Home Screen)  
![Dashboard Wireframe](./assets/dashboard_wireframe.png)  
- **Temperature and Humidity Gauges**  
- **Room Cards** – Quick access to each zone  
- **Energy Graph** – Shows energy consumption over time  
- **Alerts Section** – Warnings for high CO2, temperature spikes  

---

### 2. Room Control  
![Room Control UI](./assets/room_control_wireframe.png)  
- **Temperature Slider** – Adjust the desired temperature  
- **Mode Selector** – Cool, Heat, Auto  
- **Fan Speed** – Low, Medium, High  
- **Dehumidifier Control** – Toggle On/Off  

---

### 3. Scheduling  
![Scheduling Wireframe](./assets/scheduling_wireframe.png)  
- **Calendar View** – Create and manage daily/weekly schedules  
- **Add New Schedule** – Select room, time, and temperature  

---

## System Architecture

User ➝ Flutter App ➝ Django Backend ➝ MQTT Broker ➝ Embedded ESP32 ➝ Sensors/Actuators

- **Frontend**: Communicates with the backend via REST APIs and WebSockets.  
- **Backend**: Manages device states, schedules, and analytics.  
- **ESP32**: Collects sensor data and controls HVAC systems via MQTT.  

---

## Setup Instructions  

### 1. System Requirements  
- Linux/Mac (Windows Subsystem for Linux also supported)  
- Docker & Docker Compose  
- Python 3.8+  
- Flutter 3.0+  

---

### 2. Automated Setup (Bash Script)  
Save the following script as `setup.sh`:  
```bash
#!/bin/bash
# Full automation for project setup

PROJECT_NAME="weather_control_system"
FRONTEND_DIR="$HOME/$PROJECT_NAME/frontend"
BACKEND_DIR="$HOME/$PROJECT_NAME/backend"

echo "🚀 Setting up Weather Control App..."

# Update System
sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl python3 python3-pip python3-venv docker docker-compose build-essential unzip

# Install Flutter
git clone https://github.com/flutter/flutter.git -b stable $HOME/flutter
export PATH="$PATH:$HOME/flutter/bin"
flutter doctor

# Create Flutter App
mkdir -p $FRONTEND_DIR
cd $FRONTEND_DIR
flutter create weather_control_app

# Install Django Backend
mkdir -p $BACKEND_DIR
cd $BACKEND_DIR
python3 -m venv venv
source venv/bin/activate
pip install django djangorestframework paho-mqtt

django-admin startproject backend .
python manage.py migrate

# MQTT and ESP32 Setup
sudo apt install -y mosquitto mosquitto-clients arduino-cli esptool
sudo systemctl start mosquitto

# Docker Configuration
echo "
version: '3'
services:
  backend:
    build: ./backend
    ports:
      - '8000:8000'
  mqtt:
    image: eclipse-mosquitto
    ports:
      - '1883:1883'
" > $HOME/$PROJECT_NAME/docker-compose.yml

docker-compose up -d
echo "✅ Setup Complete!"


---

3. Run the Script

chmod +x setup.sh
./setup.sh


---

API Endpoints (Django Backend)


---

ESP32 Sample Code

void setup() {
  Serial.begin(115200);
  // Connect to WiFi and MQTT Broker
}
void loop() {
  Serial.println("Monitoring...");
  delay(1000);
}


---

Contributing

Fork the repo

Create a new branch

Submit a pull request



---

License

MIT License

---

### **How to Use**  
- **Wireframes**: Save the UI wireframes as images in the `assets/` folder.  
- **ESP32 Code**: Integrate C++ code directly into the embedded device.  
- **Frontend**: Start Flutter development with the structure created by the script.  

Would you like assistance generating the actual images or refining the ESP32 firmware next?

