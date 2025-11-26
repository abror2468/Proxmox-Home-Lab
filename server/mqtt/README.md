📡 Mosquitto MQTT Broker Installation (Ubuntu VM)

Mosquitto is used as the MQTT broker to handle communication between:

ESP32 → Server → Node-RED → InfluxDB → Grafana

📦 Step 1: Install Mosquitto and MQTT Clients
sudo apt update
sudo apt install -y mosquitto mosquitto-clients

🔁 Step 2: Enable and Start Mosquitto
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
sudo systemctl status mosquitto


You should see:

Active: active (running)

🌐 Step 3: Allow External Devices (LAN Access)

By default, Mosquitto may not accept external connections.
Create a configuration file:

sudo nano /etc/mosquitto/conf.d/listener.conf


Add this:

listener 1883
allow_anonymous true


Restart Mosquitto:

sudo systemctl restart mosquitto

🧪 Testing Mosquitto Locally (Ubuntu VM)

On your Ubuntu VM terminal, run:

mosquitto_sub -h 192.168.1.229 -t soil/test


Replace 192.168.1.229 with your VM’s actual IP if different.

Leave this terminal open.

🧪 Testing Mosquitto from Windows PC

To test publishing from a Windows machine:

⚠️ This requires Mosquitto to be installed on Windows.

Windows Publish Test:
mosquitto_pub -h 192.168.1.229 -t soil/test -m "hello from windows"


If successful, the Ubuntu terminal running mosquitto_sub should display:

hello from windows

✅ Expected System Flow

Once confirmed working, your communication chain looks like this:

ESP32 → Mosquitto → Node-RED → InfluxDB → Grafana
