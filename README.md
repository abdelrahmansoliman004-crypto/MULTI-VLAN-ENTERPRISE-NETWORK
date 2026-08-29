# Multi-VLAN Enterprise Network

> **Cisco Packet Tracer Network Architecture**  
> A comprehensive enterprise network implementing VLAN segmentation, OSPF dynamic routing, centralized DHCP and DNS services, DHCP relay, and secure remote management using SSH .

---

## 📋 Table of Contents
- [Project Overview](#-project-overview)
- [Key Network Features](#-key-network-features)
- [IP Addressing Plan](#-ip-addressing-plan)
- [Core Configurations & Services](#-core-configurations--services)
- [Security & Management](#-security--management)
- [Future Enhancements](#-future-enhancements)

---

## 🎯 Project Overview

This project implements a multi-segment enterprise network divided into four logical LANs (VLAN 10, VLAN 20, VLAN 30, and VLAN 40) using separate IPv4 /24 networks . The architecture is built around four interconnected routers that utilize OSPF to exchange routing information automatically across the topology.

---

## ✨ Key Network Features

- **Network Segmentation:** Four isolated LAN/VLAN segments utilizing distinct IPv4 /24 network address spaces .
- **Dynamic Routing:** OSPF (Area 0) is configured across the four routers to exchange routes and provide end-to-end reachability .
- **Centralized DHCP:** A single DHCP server provisions dynamic IP addresses for all four VLANs .
- **DHCP Relay:** Routers utilize the `ip helper-address` command to forward DHCP broadcast requests from remote VLANs to the centralized server .
- **Centralized Name Resolution:** A dedicated DNS server handles name resolution across all segments .
- **Secure Management:** SSH Version 2 is implemented for secure, encrypted remote router management .

---

## 📊 IP Addressing Plan

### 1. VLAN & Client Segments
| Segment | Network Address | Default Gateway | Description |
| :--- | :--- | :--- | :--- |
| **VLAN 10** | `192.168.10.0/24` | `192.168.10.1` | Server segment hosting centralized DHCP & DNS . |
| **VLAN 20** | `192.168.20.0/24` | `192.168.20.1` | Client LAN . |
| **VLAN 30** | `192.168.30.0/24` | `192.168.30.1` | Client LAN . |
| **VLAN 40** | `192.168.40.0/24` | `192.168.40.1` | Client LAN . |

### 2. Inter-Router Transit Links
| Transit Link | Network Address | Description |
| :--- | :--- | :--- |
| **R0 - R1** | `192.168.15.0/24` | Inter-router transit network . |
| **R1 - R2** | `192.168.25.0/24` | Inter-router transit network . |
| **R2 - R3** | `192.168.35.0/24` | Inter-router transit network . |

---

## ⚙️ Core Configurations & Services

### OSPF Routing (Area 0)
Each router advertises its directly connected LAN and transit networks into OSPF Area 0 . 
*   *Example on VLAN 30 Router:* Advertises networks `192.168.30.0/24`, `192.168.25.0/24`, and `192.168.35.0/24` into Area 0 .

### Centralized DHCP & DNS (VLAN 10)
All infrastructure IP services are consolidated in VLAN 10 .
*   **DHCP Server IP:** `192.168.10.10` .
*   **DNS Server IP:** `192.168.10.11` .
*   **DHCP Relay:** Router interfaces facing VLANs 20, 30, and 40 are configured with `ip helper-address 192.168.10.10` to forward Discover messages .

---

## 🔒 Security & Management

Remote administration is strictly secured using **SSH Version 2** . 
*   **Authentication:** Local authentication is enforced via `username` and `secret` commands .
*   **VTY Restrictions:** VTY lines (0 4) are restricted to SSH input only (`transport input ssh`), explicitly preventing unencrypted Telnet access .
*   **Encryption:** RSA crypto keys are generated to secure the management sessions .

---

## 🚀 Future Enhancements

To further harden the network topology, the following security features are planned for future iterations :
- Implementation of **Access Control Lists (ACLs)** for inter-VLAN traffic restriction .
- Enabling **Port Security** on access ports with a `restrict` violation mode .
- Activating **BPDU Guard** and **PortFast** on all end-device access ports .
- Administrative shutdown of all unused switch ports .
- Integration of a **Syslog server** for centralized monitoring .
- Application of password encryption and unauthorized-access MOTD banners .

## 👥 Project Team & Supervision

### 🎓 Project Team
- **Team Member 1:** Abdulrahman Amr Abdullatif Suleiman
- **Team Member 2:** Sarah Abdulrasoul Mohammed Ibrahim

### 👨‍🏫 Project Supervisor
- **Prepared for / Supervised by:** Eng. Mohamed HelmY
