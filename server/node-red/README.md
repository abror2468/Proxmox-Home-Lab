🧠 Node-RED Installation (Ubuntu VM on Proxmox)

Node-RED is used as the automation layer in this project, handling:

MQTT message processing

Data formatting

Inserting data into InfluxDB

Automation logic

📦 Step 1: Install Required Dependencies
sudo apt update
sudo apt install -y build-essential git curl

📥 Step 2: Install Node-RED (Official Installer)

This uses the official Node-RED installer for Debian/Ubuntu:

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)


When prompted:

Choose Yes to install as a service

Choose No for project features (can be enabled later)

Choose No for security (safe since this runs only on local LAN)

🔁 Step 3: Enable Node-RED on Boot
sudo systemctl enable nodered.service

▶ Start Node-RED
sudo systemctl start nodered.service

✅ Check Node-RED Status
sudo systemctl status nodered.service


You should see:

Active: active (running)

🌐 Step 4: Access Node-RED Web UI

Open in your browser:

http://<Your-Ubuntu-VM-IP>:1880


Example:

http://192.168.1.229:1880


You should now see the Node-RED editor interface.
