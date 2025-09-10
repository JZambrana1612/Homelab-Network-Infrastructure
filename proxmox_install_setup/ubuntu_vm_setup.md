# 🐧 Ubuntu VM Setup – Minecraft Server Deployment

This document outlines the setup of a virtual machine running Ubuntu Server on Proxmox VE, designed to host a Minecraft Java Edition server within the homelab environment.

---

## ⚙️ VM Configuration

- **Host Platform**: Proxmox VE 9.0 (Dell OptiPlex 7020 Micro)
- **VM OS**: Ubuntu Server 22.04 (Minimal ISO)
- **Resources Allocated**:
  - 4 vCPU cores
  - 4 GB RAM
  - 32 GB virtual disk (local-lvm)
- **Network**: Bridged (static IP configured)

---

## 🧪 Setup Process & Challenges

### ❌ Initial Failures
- First attempt to install Ubuntu Server directly failed (possible storage or memory allocation issue).
- Attempted NAS-backed installation using UGREEN NAS as attached storage — also failed.
- Switched to Alpine Linux — setup failed as well.
- Project was paused briefly due to repeated issues.

### ✅ Successful Install
- Returned to project with improved resource planning.
- Successfully installed Ubuntu Server with **4 GB of RAM** (host has 8 GB total).
- VM now boots cleanly and responds over the network.

---

## 🎮 Minecraft Server Deployment

- Created dedicated Linux user: `minecraft`
- Created isolated file directory for the server
- Installed **Java 1.21** from official package
- Downloaded Minecraft Java Edition **1.21.8** server `.jar` from official source
- Edited `server.properties`:
  - Assigned correct static IP address
  - Configured port and EULA
- Resolved early issue: IP conflict caused by overlapping DHCP reservation

---

## 🌐 Connectivity Testing

- **LAN access**: Verified from gaming PC on same subnet
- **WAN access**: Verified by remote player using dynamic DNS
- Server now supports both internal and external players

---

## 📝 Notes & Improvements (Planned)

- Backup `minecraft` user directory to UGREEN NAS
- Automate server startup on reboot
- Test other VM-hosted services using similar setup process

---

_This marks the first successful application of virtualization within the homelab._
