# Homelab Networking Project

## Overview  
This repository documents the setup and ongoing development of my personal homelab environment. The goal of this project is to gain hands-on experience with IT networking, virtualization, and self-hosting technologies while building a professional portfolio to demonstrate applied knowledge in systems administration and network design.

At its core, the homelab serves as a sandbox for experimenting with:  
- Virtualization & hypervisors (Proxmox VE)  
- Network segmentation & firewall management  
- DNS filtering & ad blocking (AdGuard)  
- Self-hosting applications and services  
- Future storage and high-availability builds  

---

## Current Setup  

### Hardware  
- **Dell OptiPlex** (repurposed) → running Proxmox VE hypervisor  
- **TP-Link Archer Router** with built-in firewall & VLAN-like segmentation  
- **TP-Link Switch** providing Ethernet connectivity & QoS for media devices (TV, PlayStation 5)  

### Configuration  
- Bootable USB flashed to install **Proxmox VE** on the OptiPlex  
- Proxmox assigned a **static IP address** for stability  
- Proper **gateway IP** configured for routing  
- **AdGuard DNS server** added for DNS-level ad blocking  
- Network segmented into **two isolated SSIDs/channels** with separate GHz bands for optimized traffic flow  

---

## Future Plans  
- Add a **dedicated NAS** for centralized storage & backups  
- Deploy a **secondary OptiPlex** for redundancy and clustering in Proxmox  
- Self-host applications (media, monitoring, automation, etc.)  
- Explore VLANs, VPN tunneling, and advanced firewall rules  

---

## Learning Objectives  
This homelab project supports my broader career development goals in IT and cybersecurity:  
- Building foundational networking knowledge (firewalls, QoS, segmentation)  
- Gaining real-world practice with virtualization technologies  
- Creating repeatable documentation for professional IT portfolios  
- Demonstrating troubleshooting and system design skills  

---

## Repository Structure  
```
/docs        → Setup notes, diagrams, and future documentation
/configs     → Example configuration files (sanitized for security)
/README.md   → Project overview
```

---

## Next Steps  
- Expand documentation with **network diagrams** (planned for `/docs`)  
- Record step-by-step setup instructions for reproducibility  
- Share lessons learned and troubleshooting tips as the homelab grows  

---

## Disclaimer  
This repository is for **educational and portfolio purposes only**. Sensitive information (such as real IP addresses, authentication keys, and personal data) has been removed or sanitized.  
