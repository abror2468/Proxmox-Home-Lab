# Server Infrastructure

This folder documents the server-side infrastructure of my home lab.
It runs on a Proxmox virtualized environment and hosts all services used for IoT, automation, and network experiments.

---

## Physical Server

**Hardware:**
- Model: Dell OptiPlex 7050 Mini
- CPU: Intel i5-6500T
- RAM: 8GB DDR4
- Storage: 500GB HDD
- Network: Ethernet via dedicated lab router and switch

**Host OS:**
- Proxmox VE 8.x

---

## Virtualization Setup

The server operates using a Proxmox virtualization stack.

### Proxmox Configuration
- Hostname: `proxmox-lab`
- Management IP: `192.168.X.50` *(masked for security)*
- Bridge Interface: `vmbr0`
- Network Type: Linux Bridge

Proxmox manages:
- Virtual Machines (VMs)
- Docker containers inside Ubuntu VMs

---

## Virtual Machines

### Primary VM: Ubuntu Server
- OS: Ubuntu Server 22.04 LTS
- vCPU: 2 cores
- RAM: 4GB
- Storage: 40GB virtual disk

This VM hosts all main services using Docker.

---

## Hosted Services

All services run inside Docker containers:

| Service | Purpose |
|--------|---------|
| Mosquitto MQTT | Message broker for IoT devices |
| Node-RED | IoT logic, automation, and flow processing |
| InfluxDB | Time-series database for sensor data |
| Grafana | Visualization and monitoring dashboard |

Each service has its own documentation folder:

- `server/mqtt/`
- `server/node-red/`
- `server/grafana/`

---

## Data Flow Architecture

The core server pipeline works like this:

ESP32 Sensors
↓
MQTT Broker (Mosquitto)
↓
Node-RED Processing
↓
InfluxDB Storage
↓
Grafana Visualization


Data is stored locally and processed in real time.

---

## Networking

- The server is connected through a dedicated lab network
- It uses a client-bridge router upstream of the main network
- VLAN expansion planned in future phases
- Remote access via VPN is planned

---

## Security Measures

Basic security practices implemented:

- SSH key authentication
- UFW firewall configured
- Sensitive credentials removed/masked from public repo
- Plans for VLAN segmentation and access restriction

---

## Problems Encountered

Documented challenges so far:

- Proxmox network bridge misconfiguration
- Docker container networking conflicts
- DNS conflicts while testing Pi-hole
- MQTT connection inconsistencies with ESP32
- Sensor value noise and calibration instability

Each issue and solution is documented as the project evolves.

---

## Future Improvements

Planned server upgrades:

- Upgrade to SSD storage
- RAM expansion to 16GB
- VLAN implementation
- Full remote VPN access
- Alert system using Node-RED
- Backup and snapshot automation
- Ansible or Terraform-based automation

---

## Screenshots & Proof

Screenshots and logs will be uploaded under:

- `server/proxmox/`
- `server/node-red/`
- `server/grafana/`
- `server/mqtt/`

These will show:
- Proxmox dashboard
- Running containers
- Node-RED flows
- Live Grafana dashboards
- MQTT service logs

---

Maintained as part of the **Proxmox Home Lab Project**


