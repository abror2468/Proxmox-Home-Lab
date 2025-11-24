# Server Infrastructure Documentation

This document covers the **technical setup and operation** of the Proxmox server used in my home lab.

This is not a high-level project overview — it is the system-level documentation for actually running and maintaining the server.

---

## 1. Host Machine Info

**Physical Server:**
- Dell OptiPlex 7050 Mini
- Intel i5-6500T
- 8GB DDR4 RAM
- 500GB HDD

**Power Usage:**  
~18W idle / ~35W under load

---

## 2. Proxmox Host Configuration

**Installed OS:** Proxmox VE 8.x  
**Host Name:** `proxmox-lab`

### Network Settings
- Bridge: `vmbr0`
- Type: Linux Bridge
- Host IP: `192.168.X.50` *(masked for security)*
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

## 3. VM Configuration

### VM: Ubuntu Server

- OS: Ubuntu Server 22.04 LTS
- vCPU: 2 cores
- RAM: 4GB
- Disk: 40GB
- Network: Bridged via vmbr0

### Inside the VM:
This VM runs Docker and all containers.

---

## 4. Docker Setup

Docker is used to manage services.

Installed using:

```bash
sudo apt install docker docker-compose -y
Docker Compose is used for container orchestration.

Main containers:

Mosquitto MQTT

Node-RED

InfluxDB

Grafana

5. Container Service Ports
Service	Port
Mosquitto MQTT	1883
Node-RED	1880
InfluxDB	8086
Grafana	3000

These ports are only accessible internally on the lab network.

6. Boot Process
Server boot order:
Proxmox boots

Ubuntu VM auto-starts

Docker service initializes

Containers auto-restart

VM auto-start enabled in Proxmox:

bash
Copy code
qm set <VMID> --onboot 1
7. Key Maintenance Commands
Check VM status:

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

No duplication. No fluff.

Just real system documentation.

---

If you want, next we can do:

✅ Proxmox README  
✅ Node-RED README  
✅ Grafana README  

Each one will be very specific and non-repetitive like this.

