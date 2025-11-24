# Proxmox Installation & VM Setup

This document describes how Proxmox VE was installed on my server using Rufus, and how Ubuntu Server was deployed as a virtual machine.

Hardware: Dell OptiPlex 7050 Mini

---

## 1. Creating Proxmox Bootable USB (Using Rufus)

### Tools Used:
- USB Flash Drive (8GB+)
- Rufus
- Proxmox VE ISO

### Steps:

1. Download Proxmox VE ISO from:
https://www.proxmox.com/en/downloads/proxmox-virtual-environment

2. Download Rufus from:
https://rufus.ie

3. Insert USB Flash Drive into PC.

4. Open **Rufus** and configure:
   - **Device:** Your USB drive
   - **Boot Selection:** Select Proxmox ISO
   - **Partition Scheme:** GPT
   - **Target System:** UEFI
   - **File System:** FAT32

5. Click **Start** and wait until the USB is made bootable.

---

## 2. Installing Proxmox on the Mini PC

1. Insert bootable USB into the OptiPlex.
2. Power on and press BIOS key (`F12`) to open Boot Menu.
3. Select the USB device.
4. Proxmox installer starts.

### Installation settings used:

- File system: ext4
- Hostname: `proxmox-lab`
- IP: Static local IP (masked for security)
- Gateway: Router IP
- Admin email: personal address
- Root password: Secure password

After installation, system rebooted directly into Proxmox VE.

---

## 3. Accessing Proxmox Web Interface

After boot:

1. Open a browser on another device.
2. Navigate to:
https://<server-ip>:8006

3. Login using:
- Username: `root`
- Password: (created during install)

---

## 4. Creating Ubuntu Server VM

### ISO Setup:
Downloaded Ubuntu Server 22.04 LTS from:
https://ubuntu.com/download/server

Upload ISO into Proxmox using:
Datacenter → Storage → Local → ISO Images → Upload

yaml
Copy code

---

### VM Creation Steps:

1. Click **Create VM**
2. Set Name: `ubuntu-lab`
3. OS: Ubuntu Server ISO
4. System:
   - BIOS: Default (SeaBIOS)
   - Storage: Default
5. Hardware:
   - CPU: 2 cores
   - RAM: 4096 MB
   - Disk: 40GB
   - Network: DHCP

6. Finish → Start VM

---

## 5. Installing Ubuntu Server on VM

1. Open VM Console
2. Follow Ubuntu installer:
   - Choose language
   - Configure network (DHCP)
   - Hostname: `ubuntu-lab`
   - Create non-root user
   - Choose OpenSSH Server
   - Use entire disk

3. Installation finished and VM rebooted successfully.

---

## 6. Accessing Ubuntu VM

After install:

You can access via:

- Proxmox Console
- SSH:
```bash
ssh user@<VM-IP>
7. VM Auto-Start Configuration
To ensure VM starts with Proxmox:

VM → Options → Start at boot = Enabled

Or via terminal:

bash
Copy code
qm set <VMID> --onboot 1
8. Current VM Purpose
This Ubuntu VM hosts:

Mosquitto MQTT

Node-RED

InfluxDB

Grafana

Installed directly on OS without containers.

9. Future Enhancements
Add second Ubuntu VM

Enable VM backup automation

VLAN lab networks

SSD upgrade for faster VM performance
