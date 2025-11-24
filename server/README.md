# Server Infrastructure Documentation

This document covers the **technical setup and operation** of my Proxmox-based home lab server.
All services run directly on an Ubuntu Server VM — not in Docker containers.

---

## 1. Host Machine (Physical Server)

**Model:** Dell OptiPlex 7050 Mini  
**CPU:** Intel i5-6500T  
**RAM:** 8GB DDR4  
**Storage:** 500GB HDD  
**Form Factor:** Mini PC  

This device functions as a 24/7 home lab server.

---

## 2. Proxmox Host Configuration

**Hypervisor:** Proxmox VE  
**Host Name:** `proxmox-lab`

### Network Configuration
- Bridge Interface: `vmbr0`
- Virtual Networking Type: Linux Bridge
- IP Address: `192.168.X.50` (masked for security)
- Gateway: `192.168.X.1`

### Network Topology

Main Router
↓
Client Bridge Router
↓
Switch
↓
Proxmox Server

yaml
Copy code

---

## 3. Virtual Machine Configuration

### Primary VM: Ubuntu Server

| Component | Value |
|--------|------|
| OS | Ubuntu Server 22.04 LTS |
| CPU | 2 cores |
| RAM | 4GB |
| Storage | 40GB |
| Network | Bridged via vmbr0 |

This VM hosts all services directly on the OS.

---

## 4. Services Running on Ubuntu VM

All services are installed directly on Ubuntu (not Docker):

| Service | Purpose | Port |
|--------|--------|------|
| Mosquitto MQTT | IoT messaging broker | 1883 |
| Node-RED | IoT logic and data processing | 1880 |
| InfluxDB | Time-series data storage | 8086 |
| Grafana | Visualization dashboard | 3000 |

Services are managed using `systemctl`.

---

## 5. System Service Control

Common commands used:

Start a service:
```bash
sudo systemctl start mosquitto
Check service status:

bash
Copy code
sudo systemctl status node-red
Enable on boot:

bash
Copy code
sudo systemctl enable grafana-server
6. Boot Process
Boot Sequence:
Physical server powers on

Proxmox starts

Ubuntu VM auto-starts

Services start sequentially via systemd

VM auto-start is enabled using:

bash
Copy code
qm set <VMID> --onboot 1
7. Current System Limitations
HDD causes slow I/O during heavy load

Limited RAM restricts number of simultaneous services

Wi-Fi bridge sometimes causes intermittent MQTT packet loss

8. Maintenance Tasks
Routine maintenance includes:

VM Snapshots before major changes

Weekly system updates using:

bash
Copy code
sudo apt update && sudo apt upgrade
Monitoring resource usage via Proxmox UI

9. Known Issues
Issue	Status
MQTT drops when WiFi unstable	Investigating
Slow disk response	Planned SSD upgrade
Node-RED crashes under high load	Being optimized

10. Planned Upgrades
Replace HDD with SSD

Upgrade RAM to 16GB

Introduce VLAN segmentation

Configure WireGuard for remote access

Add Prometheus monitoring

This document focuses only on server operation, configuration, and maintenance.
Project-level description is in the main repository README.

bash
Copy code
qm list
Start VM:

bash
Copy code
qm start <VMID>
Check running containers:

bash
Copy code
docker ps
Restart a container:

bash
Copy code
docker restart nod-red
8. Backup Strategy
Backups are planned using:

Proxmox snapshots

Weekly VM backups to external storage

Future automated scripts

9. Known Issues
Current issues and ongoing fixes:

Occasional MQTT disconnect during heavy WiFi interference

Node-RED latency spikes under high I/O

HDD limiting VM responsiveness

10. Planned Infrastructure Changes
SSD upgrade

RAM expansion to 16GB

VLAN segmentation

External Prometheus monitoring

WireGuard remote access

This document focuses strictly on server operations and infrastructure.
High-level project description is maintained in the root README.

yaml
Copy code

---

### Why this works better

Now:

Main README =  
➡ What the project is  
➡ Why you built it  
➡ What it does  

Server README =  
➡ How the server actually works  
➡ Commands  
➡ Infrastructure  
➡ Configuration  
➡ Maintenance  

