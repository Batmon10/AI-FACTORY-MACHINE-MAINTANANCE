# ShiftOptic - AI Copilot for Manufacturing Factories

ShiftOptic is an AI-powered monitoring system for small and mid-size manufacturing factories, starting with plastics and blow-molding. It provides real-time defect detection, predictive maintenance, and performance analytics.

## 🏗️ Architecture

- **Backend**: FastAPI + SQLAlchemy + PostgreSQL
- **Firmware**: ESP32 (Arduino) for sensor data collection
- **Computer Vision**: YOLOv8 for defect detection
- **MQTT Bridge**: Python service to forward sensor data
- **Dashboard**: React + Vite + Tailwind CSS + Recharts

## 📁 Project Structure

```
shiftoptic/
├── backend/          # FastAPI backend
├── firmware/         # ESP32 Arduino code
├── cv/              # Computer vision (YOLO)
├── mqtt_bridge/     # MQTT to API bridge
├── dashboard/       # React frontend
└── docker-compose.yml
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose
- Python 3.11+
- Node.js 18+ (for dashboard development)
- Arduino IDE (for ESP32 firmware)

### 1. Start Backend Services

```bash
docker-compose up -d
```

This starts:
- PostgreSQL database
- MQTT broker (Mosquitto)
- FastAPI backend
- MQTT bridge service

### 2. Setup ESP32 Firmware

1. Open `firmware/esp32/main.ino` in Arduino IDE
2. Install required libraries:
   - WiFi
   - PubSubClient
   - OneWire
   - DallasTemperature
   - ArduinoJson
3. Update WiFi credentials and MQTT broker IP
4. Upload to ESP32

### 3. Train Defect Detection Model

```bash
cd cv
pip install -r requirements.txt

# Prepare your dataset in cv/data/ following YOLO format
# Then train:
python train_defects.py
```

### 4. Run Defect Detection

```bash
cd cv
python defect_inference.py --camera 0 --machine-id 1 --display
```

### 5. Start Dashboard

```bash
cd dashboard
npm install
npm run dev
```

Dashboard will be available at `http://localhost:3000`

## 📡 API Endpoints

- `POST /api/readings` - Create a machine reading
- `GET /api/machines/{id}/latest` - Get latest reading
- `GET /api/machines/{id}/history?limit=500` - Get reading history
- `GET /api/machines/{id}/alerts` - Get recent alerts
- `GET /health` - Health check

## 🔧 Configuration

### Environment Variables

**Backend:**
- `DATABASE_URL` - PostgreSQL connection string

**MQTT Bridge:**
- `MQTT_BROKER` - MQTT broker hostname
- `MQTT_PORT` - MQTT broker port
- `BACKEND_URL` - Backend API URL

**CV Module:**
- `BACKEND_URL` - Backend API URL
- `MACHINE_ID` - Machine ID for defect events

## 🎯 Features

- **Real-time Sensor Monitoring**: Temperature, vibration, pressure
- **Defect Detection**: Computer vision-based quality control
- **Predictive Alerts**: Rule-based alerts for anomalies
- **Live Dashboard**: Real-time visualization of machine health
- **MQTT Integration**: Scalable sensor data pipeline

## 📝 Next Steps

1. Collect 100-200 labeled defect images
2. Train YOLO model on your specific defects
3. Deploy ESP32 sensors in factory
4. Configure alerts thresholds for your machines
5. Integrate with factory systems (optional)

## 🛠️ Development

### Backend Development

```bash
cd backend
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### Frontend Development

```bash
cd dashboard
npm install
npm run dev
```

## 📄 License

Proprietary - ShiftOptic

