# 🚀 OPC UA → Node-RED → InfluxDB Industrial Data Pipeline

This project demonstrates a **real-time industrial data pipeline** that retrieves machine data from an OPC UA server, processes it using Node-RED, and stores it in InfluxDB for time-series analysis.

It is designed as part of a **Cyber-Physical Systems (CPS)** workflow for machine monitoring, analytics, and future predictive maintenance.

---

## 📊 Architecture Overview

OPC UA Server → Node-RED (Processing) → InfluxDB (Storage) → Grafana (Visualization & Alerts)

---

## ⚙️ Technologies Used

* Node.js
* Node-RED
* OPC UA Protocol
* InfluxDB (v2.x)
* Grafana
* JavaScript (Function Node)

---

## 🧠 Key Features

* 🔄 Subscription-based OPC UA data acquisition
* ⚡ Real-time data processing using Node-RED
* 🧹 Data cleaning and validation (NaN/null filtering)
* 🗄️ Structured storage in InfluxDB (time-series database)
* 📊 Grafana dashboard for real-time visualization
* 🚨 Alert system for monitoring thresholds and conditions

---

---

## 🛠️ Setup Guide

### 1️⃣ Install Node.js

Download and install Node.js:
https://nodejs.org/

Verify installation:

```bash
node -v
npm -v
```

---

### 2️⃣ Install Node-RED

```bash
npm install -g --unsafe-perm node-red
```

Start Node-RED:

```bash
node-red
```

Open in browser:

```
http://127.0.0.1:1880
```

---

### 3️⃣ Install Required Node-RED Packages

In Node-RED:

* Menu → Manage Palette → Install

Install:

* node-red-contrib-opcua
* node-red-contrib-influxdb

---

### 4️⃣ Import Flow

* Open Node-RED
* Menu → Import
* Paste contents of `flows.json`
* Click **Deploy**

---

## 🔌 OPC UA Configuration

* Add multiple **OPC UA Item** nodes
* Connect them to **OPC UA Client**
* Set mode to:
  ✅ **Subscription (recommended for real-time data)**

Example machine parameters:

* Spindle Speed
* Axis Current
* Feed Rate
* Torque
* Power

---

## 🧮 Function Node Logic

The function node performs:

* Conversion of incoming values to numeric format
* Filtering invalid values (null/NaN)
* Structuring data for InfluxDB

Example:

```javascript
function toNum(v) {
    const n = (typeof v === "string") ? Number(v.trim()) : Number(v);
    return Number.isFinite(n) ? n : null;
}

const fields = {
    actSpeed: toNum(msg.payload["..."]),
    driveLoad: toNum(msg.payload["..."])
};

// Remove null values
msg.payload = {};
for (const [k, v] of Object.entries(fields)) {
    if (v !== null) msg.payload[k] = v;
}

return msg;
```

---

## 🗄️ InfluxDB Setup

### Install InfluxDB

Download:
https://www.influxdata.com/

Start InfluxDB:
open command prompt and go to the path of influxdb file and then open using command: 

```bash
.\influxd.exe
```

Open UI:

```
http://localhost:8086
```

---

### Create Configuration

1. Create **Organization**
2. Create **Bucket**
3. Generate **API Token**

---

### Configure Node-RED InfluxDB Node

* URL: `http://localhost:8086`
* Token: `<YOUR_TOKEN>`
* Organization: `<YOUR_ORG>`
* Bucket: `<YOUR_BUCKET>`

---

## 📊 Grafana Integration

* Connect Grafana to InfluxDB
* Create dashboards for machine monitoring
* Visualize:

  * Speed
  * Torque
  * Power
  * Feed rate

---

## 🚨 Alert System

* Configure alerts in Grafana
* Define thresholds for machine parameters
* Enable notifications for abnormal conditions

---

## 🔐 Security Note

⚠️ This is a demo project.

Do NOT expose:

* OPC UA endpoints
* InfluxDB tokens
* Internal machine data

For production:

* Use environment variables
* Secure API tokens
* Use VPN or internal networks

---

## ▶️ How It Works

1. OPC UA Client subscribes to machine data
2. Data is collected in Node-RED
3. Join node aggregates multiple signals
4. Function node cleans and formats data
5. InfluxDB stores time-series data
6. Grafana visualizes and monitors the system

---

## 📈 Future Work

* 🤖 **Machine Learning Integration**
  Develop predictive maintenance models and anomaly detection using collected time-series data

* 🐳 **Pipeline Containerization**
  Dockerize the full system (Node-RED, OPC UA client, InfluxDB) for scalable and portable deployment

---

## 👨‍💻 Author

**Rohit Dogra**

Master’s Student – Mechatronics & Cyber-Physical Systems
Deggendorf Institute of Technology

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!
