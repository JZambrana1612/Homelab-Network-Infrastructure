# Homelab Networking Project

## Overview  
This repository documents the setup and ongoing development of my personal homelab environment. The purpose of this project is to gain hands-on experience with IT networking, virtualization, and cybersecurity concepts while building a professional portfolio that demonstrates applied skills.  

This lab supports my career development path as I prepare for the **CompTIA Network+ certification** and pursue longer-term goals in **cybersecurity with a focus on gov-tech roles**. It also serves as a sandbox for experimenting with:  
- Virtualization & hypervisors (Proxmox VE)  
- Network segmentation & firewall management  
- DNS filtering & ad blocking (AdGuard)  
- VPN security and traffic analysis  
- Self-hosting applications and services  
- Future honeypot experiments for logging & monitoring  

---

## Hardware  

- **Dell OptiPlex Micro 7020 (Model D15U005)** → repurposed as Proxmox VE hypervisor  
- **TP-Link Archer BE400 Router** with built-in firewall and network segmentation  
- **TP-Link TL-SG705 5-Port Gigabit Switch** for Ethernet connectivity & QoS management  
- **Frontier FRX523 Fiber Optic Router (MoCA capable)** – planned repurposing for future lab use  
- **16GB USB Drive** → flashed to install Proxmox  

Planned additions:  
- **Dedicated NAS** for centralized storage & backups  
- **Secondary OptiPlex** for redundancy and Proxmox clustering  

---

## Chronological Setup Journey  

1. **Router Replacement & Segmentation**  
   - Replaced old router with **TP-Link Archer BE400**.  
   - Segmented WiFi into two networks:  
     - *Bear1*: 2.4 GHz for lower-bandwidth devices (phones, tablets).  
     - *Bear2*: 5/6 GHz for high-bandwidth devices (gaming PC, PS5, streaming).  

2. **VPN & Security Hardening**  
   - Enabled VPN using the TP-Link Tether iOS app.  
   - Reviewed DHCP IP ranges and planned static IP assignments.  
   - Prepared for Proxmox host static IP assignment.  

3. **Switch Deployment for QoS**  
   - Introduced a **TP-Link TL-SG705 unmanaged switch**.  
   - Moved wired devices (TV, PS5, PC) from router to switch.  
   - Improved bandwidth allocation and reduced latency.  
   - Benefited from built-in loop prevention to avoid broadcast storms.  

4. **Proxmox Virtualization Setup**  
   - Repurposed **Dell OptiPlex Micro 7020** (BitLocker-locked originally).  
   - Flashed a 16GB USB with the latest Proxmox version using **Rufus**.  
   - Booted via F12 menu and installed Proxmox VE.  
   - Configured:  
     - Static IP address  
     - Correct gateway  
     - AdGuard DNS for ad blocking  
   - Proxmox installer wiped BitLocker partitions and restructured disk for virtualization use.  

5. **Linux Learning & Lab Growth**  
   - Installed updates and learned basic Linux navigation commands.  
   - Installed `tree` to visualize file system structure.  
   - Relocated OptiPlex to main desk (three-monitor setup).  
   - Began planning to install **Home Assistant** and other services.  
   - Obtained a **second OptiPlex** for potential cluster builds.  
   - Future plan: add **NAS** for network storage and redundancy.  

---

## Future Plans  

- Deploy **NAS** for backups and centralized storage.  
- Expand Proxmox with a **clustered environment** (multi-node OptiPlex).  
- Configure **firewall rules** both at the router and host level.  
- Implement **virtual honeypots** to log, analyze, and learn from traffic patterns.  
- Explore **VLANs, VPN tunneling, and advanced segmentation** for real-world enterprise parallels.  

---

## Learning Objectives  

This homelab project supports my career development by helping me:  
- Build foundational networking skills (static IPs, QoS, firewalls, segmentation).  
- Gain practical experience with **Proxmox virtualization**.  
- Learn **Linux command line** through real-world application.  
- Strengthen cybersecurity awareness with **VPNs, DNS filtering, and honeypot planning**.  
- Create **repeatable documentation** for professional IT portfolios.  
- Bridge personal projects to **enterprise-level parallels** (VLANs, traffic prioritization, clustering).  

---

## Repository Structure  

```
/docs        → Setup notes, diagrams, and lab journal
/configs     → Example configuration files (sanitized for security)
/README.md   → Project overview
```

---

## Lab Journal (Changelog)  

- **2025-08-20** – Replaced router with TP-Link Archer BE400, segmented networks (Bear1, Bear2).  
- **2025-08-21** – Enabled VPN, reviewed DHCP ranges for static IP setup.  
- **2025-08-22** – Added TL-SG705 switch, moved devices for QoS improvements.  
- **2025-08-24** – Flashed USB with Proxmox, repurposed Dell OptiPlex, wiped BitLocker partitions.  
- **2025-08-25** – Installed Proxmox, set static IP, added AdGuard DNS.  
- **2025-08-25** – Installed Linux utilities (`tree`), relocated device to desk, began planning NAS and clustering.  

---

## Tools & Resources  

- **Proxmox VE** → virtualization platform  
- **TP-Link Tether App (iOS)** → VPN setup & router management  
- **ChatGPT (GPT-5.0)** → used for Linux learning, troubleshooting, and ensuring safe execution of commands  

---

## Disclaimer  
This repository is for **educational and portfolio purposes only**. Sensitive information (such as real IP addresses, authentication keys, and personal data) has been removed or sanitized.  
