🧠 Monitoring Stack Setup (InfluxDB + Grafana)

This section documents how I installed and configured InfluxDB and Grafana on my Ubuntu VM running inside Proxmox.

🚀 InfluxDB Installation (Time-Series Database)

Used as the backend for storing all sensor data (soil moisture, etc.)

📌 Steps:

Update system packages:

sudo apt update


Add InfluxData GPG key:

curl -fsSL https://repos.influxdata.com/influxdata-archive_compat.key \
| gpg --dearmor \
| sudo tee /usr/share/keyrings/influxdb-archive-keyring.gpg > /dev/null


Add InfluxDB repository:

echo "deb [signed-by=/usr/share/keyrings/influxdb-archive-keyring.gpg] https://repos.influxdata.com/ubuntu $(lsb_release -cs) stable" \
| sudo tee /etc/apt/sources.list.d/influxdb.list


Install InfluxDB:

sudo apt update
sudo apt install influxdb2 influxdb2-cli -y


Start and enable InfluxDB service:

sudo systemctl start influxdb
sudo systemctl enable influxdb
sudo systemctl status influxdb


✅ Confirmed service running: active (running)

Access the InfluxDB Web UI:

http://192.168.1.xxx:8086


(Replace xxx with your VM’s IP address)

📊 Grafana Installation (Visualization Dashboard)

Used to visualize sensor data and create dashboards.

📌 Steps:

Install required dependencies:

sudo apt update
sudo apt install -y curl gnupg apt-transport-https


Add Grafana GPG key:

curl -fsSL https://packages.grafana.com/gpg.key \
| gpg --dearmor \
| sudo tee /usr/share/keyrings/grafana.gpg > /dev/null


Add Grafana repository:

echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" \
| sudo tee /etc/apt/sources.list.d/grafana.list


Install Grafana:

sudo apt update
sudo apt install grafana -y


Enable and start Grafana server:

sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server


✅ Confirmed service running: active (running)

Access Grafana Web UI:

http://192.168.1.xxx:3000


Default login:

Username: admin
Password: admin
