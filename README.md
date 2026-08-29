# Multi-VLAN Enterprise Network

> **Cisco Packet Tracer Network Architecture**  
> A comprehensive enterprise network implementing VLAN segmentation, OSPF dynamic routing, centralized DHCP and DNS services, DHCP relay, and secure remote management using SSH[cite: 3].

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

This project implements a multi-segment enterprise network divided into four logical LANs (VLAN 10, VLAN 20, VLAN 30, and VLAN 40) using separate IPv4 /24 networks[cite: 3]. The architecture is built around four interconnected routers that utilize OSPF to exchange routing information automatically across the topology[cite: 3].

---

## ✨ Key Network Features

- **Network Segmentation:** Four isolated LAN/VLAN segments utilizing distinct IPv4 /24 network address spaces[cite: 3].
- **Dynamic Routing:** OSPF (Area 0) is configured across the four routers to exchange routes and provide end-to-end reachability[cite: 3].
- **Centralized DHCP:** A single DHCP server provisions dynamic IP addresses for all four VLANs[cite: 3].
- **DHCP Relay:** Routers utilize the `ip helper-address` command to forward DHCP broadcast requests from remote VLANs to the centralized server[cite: 3].
- **Centralized Name Resolution:** A dedicated DNS server handles name resolution across all segments[cite: 3].
- **Secure Management:** SSH Version 2 is implemented for secure, encrypted remote router management[cite: 3].

---

## 📊 IP Addressing Plan

### 1. VLAN & Client Segments
| Segment | Network Address | Default Gateway | Description |
| :--- | :--- | :--- | :--- |
| **VLAN 10** | `192.168.10.0/24` | `192.168.10.1` | Server segment hosting centralized DHCP & DNS[cite: 3]. |
| **VLAN 20** | `192.168.20.0/24` | `192.168.20.1` | Client LAN[cite: 3]. |
| **VLAN 30** | `192.168.30.0/24` | `192.168.30.1` | Client LAN[cite: 3]. |
| **VLAN 40** | `192.168.40.0/24` | `192.168.40.1` | Client LAN[cite: 3]. |

### 2. Inter-Router Transit Links
| Transit Link | Network Address | Description |
| :--- | :--- | :--- |
| **R0 - R1** | `192.168.15.0/24` | Inter-router transit network[cite: 3]. |
| **R1 - R2** | `192.168.25.0/24` | Inter-router transit network[cite: 3]. |
| **R2 - R3** | `192.168.35.0/24` | Inter-router transit network[cite: 3]. |

---

## ⚙️ Core Configurations & Services

### OSPF Routing (Area 0)
Each router advertises its directly connected LAN and transit networks into OSPF Area 0[cite: 3]. 
*   *Example on VLAN 30 Router:* Advertises networks `192.168.30.0/24`, `192.168.25.0/24`, and `192.168.35.0/24` into Area 0[cite: 3].

### Centralized DHCP & DNS (VLAN 10)
All infrastructure IP services are consolidated in VLAN 10[cite: 3].
*   **DHCP Server IP:** `192.168.10.10`[cite: 3].
*   **DNS Server IP:** `192.168.10.11`[cite: 3].
*   **DHCP Relay:** Router interfaces facing VLANs 20, 30, and 40 are configured with `ip helper-address 192.168.10.10` to forward Discover messages[cite: 3].

---

## 🔒 Security & Management

Remote administration is strictly secured using **SSH Version 2**[cite: 3]. 
*   **Authentication:** Local authentication is enforced via `username` and `secret` commands[cite: 3].
*   **VTY Restrictions:** VTY lines (0 4) are restricted to SSH input only (`transport input ssh`), explicitly preventing unencrypted Telnet access[cite: 3].
*   **Encryption:** RSA crypto keys are generated to secure the management sessions[cite: 3].

---

## 🚀 Future Enhancements

To further harden the network topology, the following security features are planned for future iterations[cite: 3]:
- Implementation of **Access Control Lists (ACLs)** for inter-VLAN traffic restriction[cite: 3].
- Enabling **Port Security** on access ports with a `restrict` violation mode[cite: 3].
- Activating **BPDU Guard** and **PortFast** on all end-device access ports[cite: 3].
- Administrative shutdown of all unused switch ports[cite: 3].
- Integration of a **Syslog server** for centralized monitoring[cite: 3].
- Application of password encryption and unauthorized-access MOTD banners[cite: 3].
