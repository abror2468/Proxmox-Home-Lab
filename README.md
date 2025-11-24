# Proxmox Home Lab

A personal Proxmox-based home lab server where I design, test, and document networking, IoT, and automation systems.

---

## Overview

This project is my physical home lab built on a Dell OptiPlex mini PC running Proxmox VE.  
It is used to host virtual machines and containers for:

- IoT monitoring and automation
- Networking experimentation
- Server virtualization
- Infrastructure testing
- Security and segmentation practice

The goal is to simulate real-world infrastructure in a small-scale environment while building hands-on engineering experience.

---

## Lab Hardware

| Component | Details |
|---------|---------|
| Server | Dell OptiPlex 7050 Mini |
| CPU | Intel i5-6500T |
| RAM | 8GB |
| Storage | 500GB HDD |
| Network | Ethernet via dedicated lab router and switch |

---

## Software Stack

- **Hypervisor:** Proxmox VE  
- **VM OS:** Ubuntu Server  
- **Containers & Services:**  
  - Mosquitto MQTT  
  - Node-RED  
  - InfluxDB  
  - Grafana  

---

## System Architecture

The current architecture of my lab system:

ESP32 Soil Sensor
↓
WiFi Network
↓
MQTT Broker (Mosquitto)
↓
Node-RED Processing
↓
InfluxDB (Time-series storage)
↓
Grafana Dashboard





All services are hosted inside Docker containers running on a Proxmox Ubuntu VM.

---

## Current Projects

### 🌱 Smart Soil Monitoring System
An automated system where soil moisture sensors connected to an ESP32 transmit real-time data to my home server.

Features:
- Real-time moisture readings from capacitive soil sensor
- MQTT message broker for communication
- Node-RED for processing & logic
- Grafana dashboard for visualization
- Future automated watering system

---

## Proof & Evidence

I document and provide proof of this lab with:

- Proxmox dashboard screenshots
- Live Grafana sensor graphs
- Node-RED flow screenshots
- MQTT logs

These will be uploaded into the repository as the project progresses.

---

## Project Goals

- Build a fully autonomous IoT monitoring system
- Implement VLAN segmentation
- Add remote access using VPN
- Add system alerts for soil dry conditions
- Expand into additional smart sensors

---

## Problems Solved So Far

I document both successes and failures for learning purposes, including:

- Running Proxmox on low-power hardware
- Network bridging configuration
- ESP32 connectivity tunneling
- Sensor calibration challenges
- Docker networking conflicts

---

## Future Improvements

- Custom PCB design for sensor board
- Docker container orchestration
- Mobile dashboard access
- Power usage optimization
- Climate monitoring expansion

---

## Author

Built and maintained by **Abror Kurbanov**  
Electrical Engineering Student | Networking & Infrastructure Focus  

