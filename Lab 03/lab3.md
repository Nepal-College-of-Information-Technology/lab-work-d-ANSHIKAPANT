# Lab 3: Visualizing IoT Sensor Data with Interactive Dashboards

---

## 1. Title
Visualizing IoT Sensor Data with Interactive Dashboards

---

## 2. Objectives
The objectives of this laboratory are to:
- Retrieve sensor readings from the REST API created in Lab 2.
- Understand the role of visualization in IoT monitoring.
- Build a web dashboard to display sensor data interactively.
- Show both real-time and historical views of temperature and humidity.
- Deploy the dashboard on AWS EC2.
- Analyze sensor behavior using graphical charts.

---

## 3. Introduction
The Internet of Things (IoT) generates a large amount of sensor data continuously. Raw values are difficult to interpret directly, so visualization is essential for understanding trends, anomalies, and system behavior.

A dashboard offers a user-friendly interface to monitor live readings and analyze historical patterns. In this lab, we developed an IoT dashboard that retrieves data from a backend API and presents it in a clear graphical form.

---

## 4. Background Theory

### 4.1 Data Visualization in IoT
Visualization converts raw sensor values into charts and graphs that are easier to understand and analyze.

### 4.2 API-Driven Architecture
The dashboard communicates with a backend service through REST APIs. This makes the system modular, scalable, and easier to maintain.

### 4.3 Dashboards
Dashboards provide real-time monitoring and historical analysis, which helps users make better decisions.

### 4.4 Data Monitoring
Monitoring allows users to observe environmental conditions and detect unusual changes quickly.

---

## 5. Tools and Technologies
- Python
- FastAPI
- Uvicorn
- TinyDB
- HTML, CSS, and JavaScript
- Chart.js
- AWS EC2
- Ubuntu Server

---

## 6. Procedure

### Step 1: Launch EC2 Instance
- Sign in to the AWS console.
- Start an Ubuntu EC2 instance.

### Step 2: Update System Packages
```bash
sudo apt update && sudo apt upgrade -y
```

### Step 3: Install Required Packages
```bash
sudo apt install python3-pip python3-venv -y
```

### Step 4: Create Project Folder
```bash
mkdir iot-dashboard && cd iot-dashboard
```

### Step 5: Create a Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 6: Install Python Libraries
```bash
pip install fastapi uvicorn tinydb python-multipart
```

### Step 7: Project Structure
```text
iot-dashboard/
├── main.py
├── db.json
├── venv/
└── static/
    └── index.html
```

### Step 8: Backend Code
```python
from fastapi import FastAPI
from tinydb import TinyDB
from datetime import datetime
from fastapi.staticfiles import StaticFiles
from fastapi.responses import FileResponse
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

db = TinyDB("db.json")
app.mount("/static", StaticFiles(directory="static"), name="static")

@app.get("/")
def root():
    return {"status": "Dashboard API Active"}

@app.get("/dashboard")
def dashboard():
    return FileResponse("static/index.html")

@app.post("/weather")
def add_weather(temperature: float, humidity: float):
    record = {
        "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "temperature": temperature,
        "humidity": humidity
    }
    db.insert(record)
    return {"message": "entry stored", "data": record}

@app.get("/weather")
def get_weather():
    return db.all()
```

### Step 9: Frontend Dashboard
```html
<!DOCTYPE html>
<html>
<head>
    <title>IoT Dashboard</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body { font-family: Arial; background: #eef2f7; margin: 0; }
        header { background: #1e3c72; color: #fff; padding: 15px; text-align: center; }
        .cards { display: flex; justify-content: space-around; margin: 20px; }
        .card { background: #fff; padding: 20px; width: 40%; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); text-align: center; }
        .value { font-size: 28px; font-weight: bold; margin-top: 10px; }
        canvas { margin: 20px; background: #fff; padding: 10px; border-radius: 8px; }
    </style>
</head>
<body>
<header>IoT Sensor Dashboard</header>
<div class="cards">
    <div class="card"><h3>Temperature</h3><div id="temp" class="value">-- °C</div></div>
    <div class="card"><h3>Humidity</h3><div id="hum" class="value">-- %</div></div>
</div>
<canvas id="chart"></canvas>
<script>
let chart;
async function refresh() {
    const res = await fetch("/weather");
    const data = await res.json();
    if (!data.length) return;
    const latest = data[data.length - 1];
    document.getElementById("temp").innerText = latest.temperature + " °C";
    document.getElementById("hum").innerText = latest.humidity + " %";
    const labels = data.map(d => d.timestamp);
    const temps = data.map(d => d.temperature);
    if (chart) chart.destroy();
    chart = new Chart(document.getElementById("chart"), {
        type: "line",
        data: { labels, datasets: [{ label: "Temperature", data: temps, borderColor: "red", fill: false }] }
    });
}
refresh();
setInterval(refresh, 5000);
</script>
</body>
</html>
```

### Step 10: Run the Server
```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

### Step 11: Test the Deployment
- Open the dashboard at:
  http://<EC2-Public-IP>/dashboard
- Open the API at:
  http://<EC2-Public-IP>/weather

---

## 7. Results
- The REST API was successfully deployed on AWS EC2.
- Sensor readings were stored and retrieved through TinyDB.
- The dashboard displayed live temperature and humidity values.
- Historical data was visualized using Chart.js.
- The system demonstrated the importance of dashboards in IoT monitoring.

---

## 8. Output
- Successful deployment of the dashboard.
- Interactive visualization of sensor data.
- Real-time and historical monitoring capability.
- Better understanding of IoT data analysis.

---

## 9. Screenshot Gallery

### Screenshot 1
<img src="./Screenshot%202026-06-23%20223124.png" alt="Lab 3 Screenshot 1" width="700" />

### Screenshot 2
<img src="./Screenshot%202026-07-07%20202005.png" alt="Lab 3 Screenshot 2" width="700" />

---

## 10. Conclusion
This lab demonstrated how IoT sensor data can be visualized through an interactive dashboard. The use of FastAPI for backend services and Chart.js for frontend visualization made it possible to monitor temperature and humidity effectively. The project highlights the importance of dashboards in transforming raw sensor data into meaningful information for monitoring and decision-making.
