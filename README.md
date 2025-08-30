# Homelab Networking Project

## Overview  
This repository documents the setup and ongoing development of my personal homelab environment. The purpose of this project is to gain hands-on experience with IT networking, virtualization, and cybersecurity concepts while building a professional portfolio that demonstrates applied skills.  

This lab supports my career development path as I prepare for the **CompTIA Network+ certification** and pursue longer-term goals in **cybersecurity with a focus on gov-tech roles**. It also serves as a sandbox for experimenting with:  
- Virtualization & hypervisors (Proxmox VE)  
- Network segmentation & firewall management  
- DNS filtering & ad blocking (AdGuard)  
- VPN security and traffic analysis  
- Self-hosting applications and services  
- Honeypot experiments (future, in a safe Azure environment)  

---

## Hardware  

- **Dell OptiPlex Micro 7020** → repurposed as Proxmox VE hypervisor  
- **TP-Link Archer BE6500 Router** with built-in firewall and network segmentation  
- **TP-Link TL-SG705 5-Port Gigabit Switch** for Ethernet connectivity & QoS management  
- **Frontier FRX523 Fiber Optic Router (MoCA capable)** – planned repurposing for future lab use  
- **16GB USB Drive** → flashed to install Proxmox  

Planned additions:  
- **Dedicated NAS** for centralized storage & backups (needed to continue scaling lab projects)  
- **Secondary OptiPlex** for redundancy and Proxmox clustering  

---

1. Router Replacement & Segmentation
    - Replaced old router with **TP-Link Archer BE6500**.  
    - Configured Wi-Fi with two active networks:  
      - **Bear**: Legacy 2.4 GHz / 5 GHz SSID for general-purpose and non–Wi-Fi 7 devices (phones, tablets, IoT, older laptops).  
      - **Bear_MLO**: Wi-Fi 7 Multi-Link Operation (5/6 GHz) SSID dedicated to high-bandwidth, latency-sensitive devices (gaming PC, PS5, streaming).  
    - Security:  
      - **Bear_MLO** secured with WPA3-Personal for modern compatibility and performance.  
      - **Bear** retained for backward compatibility with devices that do not yet support WPA3 or Wi-Fi 7.  
    - Router firewall & security:  
      - Enabled SPI Firewall for stateful packet inspection.  
      - Disabled WAN ping responses to reduce external visibility.  
      - Reviewed Access Control, ALG, and Device Isolation features.  
      - Planned to enable **IP & MAC Binding** for Proxmox and NAS to prevent ARP spoofing (pending).

2. **VPN & Security Hardening**  
    - Enabled OpenVPN server on TP-Link Archer BE6500.  
    - Generated VPN certificate and exported client configuration file.  
    - Set up TP-Link DDNS for dynamic IP resolution.  
    - Imported `.ovpn` profile into OpenVPN Connect client and confirmed remote tunnel connectivity.  
    - Documented sanitized VPN screenshots and created dedicated `vpn_setup/` with supporting links.  
    - Reviewed router firewall and security settings (SPI Firewall, Access Control, ALGs, Device Isolation).  
    - Planned to enable IP & MAC Binding for Proxmox host and NAS to prevent ARP spoofing (pending).

3. **Switch Deployment for QoS**  
   - Introduced a **TP-Link TL-SG705 unmanaged switch**.  
   - Moved wired devices (TV, PS5, PC) from router to switch.  
   - Improved bandwidth allocation and reduced latency.  
   - Benefited from built-in loop prevention to avoid broadcast storms.  

4. **Proxmox Virtualization Setup**     
   - Repurposed **Dell OptiPlex Micro 7020** (originally BitLocker-locked).  
    - Flashed a 16GB USB with the latest Proxmox VE ISO using **Rufus**.  
    - Booted via F12 boot menu and installed Proxmox VE.  
    - Configured during installation:  
        - Static IP address  
        - Correct gateway  
        - AdGuard DNS for ad blocking  
    - Proxmox installer wiped BitLocker partitions and restructured disk for virtualization use.  
    - Installed basic Linux utilities (e.g., `tree`) for navigation and system management.  
    - Partitioned 14GB to `lxc-storage (pve)` for testing; determined storage is insufficient for self-hosting apps (awaiting NAS expansion).  
    - Relocated device to primary desk setup with three-monitor configuration and began planning clustering/NAS integration.    

5. **Linux Learning & Lab Growth**  
   - Installed updates and learned basic Linux navigation commands.  
   - Installed `tree` to visualize file system structure.  
   - Relocated OptiPlex to main desk (three-monitor setup).  
   - Began planning to install **Home Assistant** and other services.  
   - Obtained a **second OptiPlex** for potential cluster builds.  

6. **Storage Limitation**  
   - Partitioned **14GB** to `lxc-storage (pve)` for project use.  
   - Current capacity is insufficient for self-hosting applications.  
   - Plan: wait until a **dedicated NAS device** is added before proceeding with larger projects.  

---

## Future Plans  

- Deploy **NAS** for backups and centralized storage.  
- Expand Proxmox with a **clustered environment** (multi-node OptiPlex).  
- Configure **firewall rules** both at the router and host level.  
- Implement **virtual honeypots** (planned in Azure) to log and analyze traffic safely.  
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
home-lab/
│
├── VPN_setup/
│   ├── tplink_VPN_setup.md
│   └── vpn_links.md
|
├── images/
│   └── proxmox/
│   |   ├── Rufus_Proxmox_flash_setup.png
│   |   ├── VFree_space.png
│   |   ├── add_storage_directory.png
│   |   ├── mount_persistence.png
│   |   ├── proxmox_homepage.png
│   |   ├── proxmox_login.png
│   |   └── tplink_dhcp_settings.png
│   └── vpn/
│   |   ├──DDNS_setup.png
│   |   ├── enable_openvpn.png
│   |   ├── openvpn_connect_startup.png
│   |   ├── openvpn_connection_check.png
│   |   ├── openvpn_startup2.png
│   |   ├── openvpn_startup_connected.png
│   |   ├── openvpn_startup_connected2.png
│   |   └── vpn_export.png
│
├── proxmox_install_setup/
│   ├── identify_dhcp_gateway.md
│   ├── links.md
│   ├── proxmox_install_setup_guide.md
│   └── proxmox_lxc_storage_setup.md
│
├── README.md
```

---

## Lab Journal (Changelog)  

- **2025-08-20** — Replaced router with TP-Link Archer BE6500, segmented networks (Bear, Bear_MLO).  
- **2025-08-21** — Enabled VPN, reviewed DHCP ranges for static IP setup.  
- **2025-08-22** — Added TL-SG705 switch, moved devices for QoS improvements.  
- **2025-08-24** — Flashed USB with Proxmox, repurposed Dell OptiPlex, wiped BitLocker partitions.  
- **2025-08-25** — Installed Proxmox, set static IP, added AdGuard DNS.  
- **2025-08-25** — Installed Linux utilities (`tree`), relocated device to desk, began planning NAS and clustering.  
- **2025-08-25** — Partitioned 14GB to `lxc-storage (pve)`; storage too limited for self-hosting apps, awaiting NAS.  
- **2025-08-26** — Configured OpenVPN server on Archer BE400. Generated certificate, set up TP-Link DDNS, exported client config, and confirmed remote VPN tunnel working.  
- **2025-08-26** — Documented sanitized VPN screenshots and created dedicated `vpn_setup/` with links/resources.  
- **2025-08-26** — Reviewed Archer firewall & security options (SPI, Access Control, IP & MAC Binding, Device Isolation). Decided to enable IP/MAC binding later for Proxmox/NAS.  

---

## Tools & Resources

- **Proxmox VE** → virtualization platform  
- **TP-Link Tether App (iOS)** → VPN setup & router management  
- **OpenVPN Connect** → client software for VPN testing  
- **ChatGPT (GPT-5.0)** → used for Linux learning, troubleshooting, VPN setup documentation, and safe execution of commands  

---

## Disclaimer  
This repository is for **educational and portfolio purposes only**. Sensitive information (such as real IP addresses, authentication keys, and personal data) has been removed or sanitized.  

# Lab Notes & Next Notes To Capture 
- Adding a NAS device for extended storage.  
- Setting up Home Assistant as first hosted service.
  - Current storage amount is not sufficient for hosting virtual environment containers & capabilities
- Exploring VLANs and firewall rule sets.
  - Noticed on my current router, the firewall capabilities are very baseline and don't allow for much configuration
  - Potential separate physical firewall may have to be considered

---
