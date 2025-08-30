# 🏡 Home-Lab Project

This repository documents the setup and ongoing development of my personal homelab environment. The purpose of this project is to gain hands-on experience with IT networking, virtualization, and cybersecurity concepts while building a professional portfolio that demonstrates applied skills.  

This lab supports my career development path as I prepare for the **CompTIA Network+ certification** and pursue longer-term goals in **networking & cybersecurity**.

---

## 📌 Current Environment

### Router & Wireless Segmentation
- TP-Link Archer BE6500 (Wi-Fi 7) deployed as core router.  
- **SSID_MLO** → WPA3-only, for modern/high-bandwidth devices (gaming PC, PS5, Proxmox).  
- **SSID_NAME** → WPA2/WPA3 mixed mode, fallback for legacy/IoT devices.  
- Security measures applied:  
  - WPA3 prioritized, legacy fallback limited  
  - WPS disabled  
  - DNS over TLS with AdGuard DNS  
  - EasyMesh disabled  
  - Remote management disabled  
  - SPI Firewall enabled, WAN ping disabled  

[➡ View full router security & optimization notes](router_security.md)

### Switch
- TP-Link TL-SG705 unmanaged switch.  
- Provides Ethernet connectivity for PC, PS5, and TV.  
- Improves QoS and reduces latency vs direct router connection.  

### Proxmox Virtualization
- Running on Dell OptiPlex 7020 Micro (repurposed from BitLocker lock).  
- Installed **Proxmox VE 9.0** via bootable USB (Rufus).  
- Configured:  
  - Static IP addressing  
  - Correct gateway and DNS (AdGuard)  
  - Wiped legacy partitions and allocated storage for virtualization.  
- Added basic Linux tools (`tree`) for navigation.  
- Partitioned 14GB to `lxc-storage (pve)` (not sufficient for hosting — NAS planned).  

### VPN
- OpenVPN server configured directly on the Archer BE6500.  
- Certificate generated and exported with DDNS hostname.  
- Client profile imported into OpenVPN Connect.  
- Remote testing verified: LAN access works, IP routing confirmed.  
- Documented sanitized screenshots of connection process.  

---

## 🛠️ Tools & Resources
- **Proxmox VE** — virtualization platform.  
- **OpenVPN Connect** — client used for VPN testing.  
- **TP-Link Tether (iOS)** — router management app.  
- **AdGuard DNS** — secure DNS filtering over TLS.  
- **ChatGPT (GPT-5.0)** — used for guided troubleshooting, documentation, and validation of commands.  

---

## 📓 Lab Journal (Changelog)

- **2025-08-20** — Replaced router with TP-Link Archer BE6500, segmented SSIDs (SSID_NAME, SSID_MLO).  
- **2025-08-21** — Reviewed DHCP ranges for static IP assignment.  
- **2025-08-22** — Added TL-SG705 switch, moved devices for QoS improvements.  
- **2025-08-24** — Flashed USB with Proxmox VE, repurposed Dell OptiPlex, wiped BitLocker partitions.  
- **2025-08-25** — Installed Proxmox, set static IP, configured AdGuard DNS.  
- **2025-08-25** — Installed Linux utilities (`tree`), relocated device to desk, began planning NAS and clustering.  
- **2025-08-25** — Partitioned 14GB for `lxc-storage (pve)`; determined insufficient for self-hosting apps (NAS planned).  
- **2025-08-26** — Configured OpenVPN server on Archer BE6500. Generated certificate, set up TP-Link DDNS, exported client config, and confirmed remote VPN tunnel working.  
- **2025-08-26** — Documented VPN screenshots and created dedicated `vpn_setup/` folder with guides and links.  
- **2025-08-26** — Reviewed Archer firewall/security (SPI, Access Control, IP/MAC binding, Device Isolation). Planned future IP/MAC binding for Proxmox/NAS.  
- **2025-08-29** — ISP upgraded from Spectrum 500 Mbps to Frontier Fiber 1 Gbps symmetric. Enabled testing of VPN in full-tunnel mode and improved latency for Wi-Fi 7 segmentation.  

---

## 🚧 Future Plans

- Deploy **NAS** for backups and centralized storage.  
- Expand Proxmox into a **clustered environment** with multiple OptiPlex nodes.  
- Enable **IP/MAC Binding** for critical hosts (Proxmox, NAS, main PC).  
- Configure **manual port forwarding** (replace UPnP) for gaming services (PS5, Steam, Epic).  
- Implement **VLAN segmentation** (Homelab / IoT / Personal).  
- Migrate LAN subnet from **192.168.0.0/24 → 192.168.10.0/24** for cleaner addressing.  
- Evaluate **pfSense/OPNsense** (dedicated or VM) for IDS/IPS and advanced firewall rules.  
- Deploy **virtual honeypots** (via Proxmox or Azure) for traffic logging and analysis.  

---

## 📂 Repository Structure

```plaintext
├── VPN_setup/
│   ├── tplink_VPN_setup.md
│   ├── vpn_links.md
│
├── proxmox_install_setup/
│   ├── proxmox_install_setup_guide.md
│   ├── proxmox_links.md
│   ├── identify_dhcp_gateway.md
│   ├── proxmox_lxc_storage_setup.md
│
├── router_security.md
│
├── images/
│   ├── vpn/
│   ├── proxmox/
│   ├── router/
│
└── README.md
```

---

## ⚡ Summary

This homelab demonstrates practical networking, virtualization, and security skills using consumer hardware with enterprise concepts.  
It serves as a **portfolio project** to showcase:  
- Network segmentation (SSID strategy, VLAN planning).  
- VPN deployment and testing.  
- Virtualization with Proxmox VE.  
- Security hardening on consumer routers.  
- Documentation of lessons learned and future roadmap. 
