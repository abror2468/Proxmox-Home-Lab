📦 InfluxDB Installation (Ubuntu VM)

This installs InfluxDB 2.x on an Ubuntu VM running on Proxmox.

1️⃣ Add InfluxDB repository + key
sudo apt update

curl -fsSL https://repos.influxdata.com/influxdata-archive_compat.key \
| gpg --dearmor \
| sudo tee /usr/share/keyrings/influxdb-archive-keyring.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/influxdb-archive-keyring.gpg] https://repos.influxdata.com/ubuntu $(lsb_release -cs) stable" \
| sudo tee /etc/apt/sources.list.d/influxdb.list

2️⃣ Install InfluxDB
sudo apt update
sudo apt install influxdb2 influxdb2-cli -y

3️⃣ Start and enable InfluxDB
sudo systemctl start influxdb
sudo systemctl enable influxdb
sudo systemctl status influxdb


You should see:

active (running)

4️⃣ Access InfluxDB Web UI

Open in your browser:

http://192.168.1.xxx:8086


(Replace xxx with your VM’s real IP)

📊 Grafana Installation (Ubuntu VM)

This installs Grafana OSS.

1️⃣ Install dependencies
sudo apt update
sudo apt install -y curl gnupg apt-transport-https

2️⃣ Add Grafana repository + key
curl -fsSL https://packages.grafana.com/gpg.key \
| gpg --dearmor \
| sudo tee /usr/share/keyrings/grafana.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" \
| sudo tee /etc/apt/sources.list.d/grafana.list

3️⃣ Install and start Grafana
sudo apt update
sudo apt install grafana -y

sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server


✅ Status should show: active (running)

4️⃣ Access Grafana Web UI

Open in your browser:

http://192.168.1.xxx:3000


Default login:

Username: admin
Password: admin
