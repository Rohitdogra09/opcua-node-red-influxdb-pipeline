# 🚀 OPC UA → Node-RED → InfluxDB Pipeline

This project demonstrates a real-time industrial data pipeline that retrieves machine data from an OPC UA server, processes it using Node-RED, and stores it in InfluxDB for time-series analysis.

---

## 📊 Architecture Overview

OPC UA Server → Node-RED (Processing) → InfluxDB (Storage)

---

## ⚙️ Technologies Used

* Node.js
* Node-RED
* OPC UA Protocol
* InfluxDB (v2.x)
* JavaScript (Function Node)

---

## 🧠 Features

* Subscription-based OPC UA data acquisition
* Real-time data processing using Node-RED
* Filtering invalid values (NaN/null handling)
* Structured data storage in InfluxDB
* Scalable architecture for industrial CPS systems

---

## 📷 Screenshots

### Node-RED Flow

![Flow](screenshots/flow.png)

### Function Node Logic

![Function](screenshots/function_node.png)

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
Menu → Manage Palette → Install:

* node-red-contrib-opcua
* node-red-contrib-influxdb

---

### 4️⃣ Import Flow

* Open Node-RED
* Menu → Import
* Paste contents of `flows.json`
* Deploy

---

## 🔌 OPC UA Configuration

* Add multiple **OPC UA Item** nodes
* Connect to **OPC UA Client**
* Set mode to:
  ✅ **Subscription (recommended)**

Example data points:

* Spindle speed
* Axis current
* Feed rate
* Torque
* Power

---

## 🧮 Function Node Logic

The function node:

* Converts values to numbers
* Filters invalid values
* Builds structured payload for InfluxDB

Key logic:

```javascript
function toNum(v) {
    const n = (typeof v === "string") ? Number(v.trim()) : Number(v);
    return Number.isFinite(n) ? n : null;
}
```

---

## 🗄️ InfluxDB Setup

### Install InfluxDB

Download:
https://www.influxdata.com/

Run InfluxDB server:

```bash
influxd
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

## 🔐 Security Note

⚠️ This is a demo project.

Do NOT expose:

* OPC UA endpoint publicly
* InfluxDB tokens
* Internal machine data

Use environment variables for production.

---

## ▶️ How It Works

1. OPC UA Client subscribes to machine data
2. Data is collected in Node-RED
3. Join node aggregates values
4. Function node cleans & formats data
5. InfluxDB node writes data to time-series database

---

## 📈 Future Improvements

* Add Grafana dashboard
* Add alert system
* Add anomaly detection (AI/ML)
* Dockerize the pipeline

---

## 👨‍💻 Author

**Rohit Dogra**

Master’s Student – Mechatronics & Cyber-Physical Systems
Deggendorf Institute of Technology

---

## ⭐ If you like this project

Give it a star ⭐ on GitHub!
