# 🏦 Multi-Branch Bank Network Design

A multi-branch banking network topology simulated in **Cisco Packet Tracer**, connecting a central office to 8 regional branch offices with dynamic routing, loop-free switching, and centralized enterprise server services.

---

## 📋 Overview

This project models enterprise-grade inter-branch connectivity for a banking organization. Each branch operates on an isolated IPv4 subnet with static host addressing and communicates with both peer branches and centralized banking servers through a hierarchical router topology.

### Key Features
- **Multi-Branch Architecture:** 1 Central Office + 8 Branch LANs (40 end-user workstations total).
- **Dynamic Routing:** Hybrid routing implementation using **EIGRP** and **RIP** across 10 routers for automated route discovery and inter-branch reachability.
- **Switching & Loop Prevention:** **PVST (Per-VLAN Spanning Tree)** enabled across all 8 branch switches.
- **Centralized Server Services:** Hosted on `Server0` (`172.20.0.248`), providing **HTTP, HTTPS, DNS, FTP, TFTP, NTP, and Syslog**.

---

## 🏗️ Network Topology & Components

| Component | Quantity | Role / Notes |
| :--- | :---: | :--- |
| **Routers** | 10 | `Router0` (Central Core), `Router10` (Intermediate Distribution for Routers 5, 6, 7), and 8 Branch Edge Routers |
| **Switches** | 8 | One access switch per branch office running PVST |
| **End Devices (PCs)** | 40 | 5 static-IP workstations per branch |
| **Central Server** | 1 | `Server0` connected to the Central Core (`Router0`) |
| **Power Distribution** | 3 | Infrastructure power distribution units |

---

## 🌐 IP Addressing & Subnetting Scheme

All subnets use a `/21` subnet mask (`255.255.248.0`).

### Central Office
| Device | Interface / Role | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Router0** | Central Core LAN | `172.20.0.1` | `255.255.248.0` | — |
| **Server0** | Central Services | `172.20.0.248` | `255.255.248.0` | `172.20.0.1` |

### Branch Networks
| Branch | Edge Router | Switch | Default Gateway | PC IP Address Range |
| :---: | :--- | :--- | :--- | :--- |
| **Branch 1** | `Router13` | `Switch5` | `172.20.16.1` | `172.20.16.2` – `172.20.16.6` |
| **Branch 2** | `Router14` | `Switch19` | `172.20.32.1` | `172.20.32.2` – `172.20.32.6` |
| **Branch 3** | `Router17` | `Switch6` | `172.20.48.1` | `172.20.48.2` – `172.20.48.6` |
| **Branch 4** | `Router7` | `Switch12` | `172.20.88.1` | `172.20.88.2` – `172.20.88.6` |
| **Branch 5** | `Router6` | `Switch11` | `172.20.96.1` | `172.20.96.2` – `172.20.96.6` |
| **Branch 6** | `Router5` | `Switch17` | `172.20.104.1` | `172.20.104.2` – `172.20.104.6` |
| **Branch 7** | `Router3` | `Switch3` | `172.20.120.1` | `172.20.120.2` – `172.20.120.6` |
| **Branch 8** | `Router4` | `Switch1` | `172.20.152.1` | `172.20.152.2` – `172.20.152.6` |

---

## 🧪 Verification & Testing

End-to-end connectivity was verified using **ICMP Echo Requests (`ping`)** between central infrastructure and branch workstations:
- `Server0 (172.20.0.248)` $\leftrightarrow$ `PC5 (172.20.16.6)` — **Success**
- `PC7 (172.20.16.4)` $\rightarrow$ `Server0 (172.20.0.248)` — **Success**

---

## 🚀 Future Enhancements
- Departmental **VLAN segmentation** (e.g., Teller, Admin, Guest, Server VLANs) with Inter-VLAN routing.
- Automated IP allocation via **DHCP** pools/relay agents.
- Enhanced security using **Access Control Lists (ACLs)**, port security, and SSH management.
- WAN link redundancy and failover paths.

---


