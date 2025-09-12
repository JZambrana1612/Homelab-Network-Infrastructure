# VPN Setup with OpenVPN on TP-Link Archer BE400

This section documents the process of setting up a secure VPN for remote access to the homelab environment using the built-in OpenVPN server on the TP-Link Archer BE6500 router.  

---

## 1. Configure Dynamic DNS (DDNS)
Before enabling the VPN, set up DDNS so your exported configuration file references a hostname instead of a changing ISP IP address.  

- Navigate to **Advanced → Network → Dynamic DNS**.  
- Choose **TP-Link DDNS** (free option).  
- Log in with your TP-Link ID.  
- Register a hostname (e.g., `homelab.tplinkdns.com`).  
- Bind and activate it.  

![DDNS Setup](../images/vpn/DDNS_setup.png)

Once enabled, the router will automatically update TP-Link whenever your ISP changes your home IP.

### Important Note on Dynamic DNS
If your ISP provides a dynamic public IP (changes weekly/monthly), your `.ovpn` file will break unless you use a Dynamic DNS (DDNS) hostname.  
We configured our router’s built-in TP-Link DDNS (`hostname.tplinkdns.com`) and updated the `.ovpn` file with that hostname.  
This ensures that the VPN remains accessible even after router resets or IP changes.  

---

## 2. Generate a Certificate
The OpenVPN server requires a certificate for encryption and authentication. This must be done before enabling the server.  

- Navigate to **Advanced → VPN Server → OpenVPN**.  
- In the **Certificate** section, click **Generate**.  
- Wait for the process to complete (this may take a few minutes).

---

## 3. Enable the OpenVPN Server
- Still under **Advanced → VPN Server → OpenVPN**, check **Enable VPN Server**.  
- Configure:  
  - **Service Port**: Default `1194` (UDP recommended).  
  - **Protocol**: UDP (faster) or TCP (fallback if blocked).  
  - **VPN Subnet**: Default is `10.8.0.0/24` (can leave as is).  
  - **Client Access**: Choose between *Home Network Only* or *Home Network + Internet*.  

![Enable OpenVPN](../images/vpn/enable_openvpn.png)

  - **Selected Mode**: This homelab now uses **Home Network + Internet** (full-tunnel) to encrypt all traffic through the home network.

---

## 4. Export the OpenVPN Configuration File
- After enabling the server and certificate, click **Export Config**.  
- This downloads a `.ovpn` file containing:  
  - Your DDNS hostname.  
  - Encryption keys and certificates.  
  - Port and protocol information.  

![Export Configuration](../images/vpn/vpn_export.png))

## 🔧 Visual Guide: Fine-Tuning Your `.ovpn` File

When editing your exported `.ovpn` file, make sure to update it with the highlighted lines below.  
These small adjustments ensure your VPN connection stays stable, even if your public IP changes or your router resets.

![Fine-Tuned OVPN Config](../images/vpn/ovpn_finetune.png)

Note: Some values in the screenshot (hostname/port) are intentionally redacted for security. Since more than likely you've already downloaded OpenVPN on your device, please open the `.ovpn` file with  a service such as *Visual Studio Code* to edit the file as shown above.

### Why This Matters
- ✅ Using your **Dynamic DNS hostname** (instead of a raw IP) ensures the VPN always points to your current public IP.  
- ✅ Adding **custom DNS options** (like AdGuard or your preferred DNS) helps with reliable name resolution and filtering.  

> ⚠️ Without these adjustments, your VPN may stop working the next time your ISP refreshes your IP.

---

## 5. Import Config to OpenVPN Client
- Download and install [OpenVPN Connect](https://openvpn.net/client/).  
- Import the `.ovpn` file on your laptop or phone.  
- Connect using your router’s credentials.  

![OpenVPN Client](../images/vpn/openvpn_connect_startup.png) -> ![OpenVPN Client](../images/vpn/openvpn_startup2.png)

---

## 6. Testing the VPN
- Disconnect from home Wi-Fi and connect via mobile hotspot or hotel Wi-Fi.  
- Launch the OpenVPN client and connect.  
- Confirm:  
  - You can reach LAN devices (Proxmox, NAS, etc.).  
  - Your browsing IP shows your home ISP if using full tunnel mode.  

![Testing VPN](../images/vpn/openvpn_startup_connected.png) -> ![Lower Section](../images/vpn/openvpn_startup_connected2.png)
--
*You can also test the connection via *[Whatismyip](https://www.whatismyip.com/)**
--
![Connection Check](../images/vpn/openvpn_connection_check.png)

  - This behavior confirms the homelab's current configuration: **full-tunnel routing is enabled.**

---

## Notes
- **Security:** Treat the `.ovpn` file like a password. Store securely (USB, encrypted vault).  
- **Modes:**  
  - *Home Network Only*: Only access LAN devices. Faster on limited upload speeds.  
  - *Home Network + Internet*: Encrypts *all* traffic through home network. Best when using Fiber or on untrusted Wi-Fi.  
    **→ Currently active mode in this homelab.**
- **Next Steps:**
  - Address current VPN limitations: the TP-Link BE6500 router provides a stable OpenVPN server, but lacks advanced **inter-VLAN routing** and **wireless SSID tagging**. This means VPN traffic can only be segmented effectively over Ethernet.  
  - To overcome this, we’re evaluating a **virtualized firewall** (pfSense or OPNsense) for features like IDS/IPS, deeper traffic inspection, and more flexible VPN handling.  
  - For a more user-friendly path, we’re also considering **Firewalla’s Cybersecurity Gold line**, which simplifies advanced security policies while maintaining enterprise-grade protection.  
  - Finally, adding a **TP-Link Omada access point** would allow us to extend VLAN tagging into the **wireless environment**, ensuring VPN users on Wi-Fi benefit from the same segmentation and security controls as wired devices.

---
