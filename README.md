# 🌐 Enterprise Network Infrastructure Design

### CCNA Networking Project — VLANs, DHCP, EIGRP, ACLs & Network Security

![Cisco](https://img.shields.io/badge/Cisco-Networking-1BA0D7?style=for-the-badge\&logo=cisco\&logoColor=white)
![CCNA](https://img.shields.io/badge/CCNA-Enterprise%20Networking-red?style=for-the-badge)
![Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-Lab-blue?style=for-the-badge)
![Networking](https://img.shields.io/badge/Networking-Infrastructure-green?style=for-the-badge)

## 📌 Project Overview

This project presents the **design, implementation, configuration, and testing of a complete enterprise network infrastructure** based on core Cisco CCNA concepts.

The network simulates a real-world organization containing multiple **routers, switches, servers, wireless access points, and end devices**. Different departments are logically segmented using VLANs, while routing, network services, security, and remote management are integrated to create a functional enterprise environment.

The project brings together several networking technologies into one complete topology, including:

* VLANs & VLAN Segmentation
* IEEE 802.1Q Trunking
* Router-on-a-Stick (ROAS)
* Inter-VLAN Routing
* DHCP & DHCP Relay
* Static Routing
* EIGRP Dynamic Routing
* Rapid Spanning Tree Protocol (RSTP)
* SSH Remote Management
* AAA Authentication
* RADIUS Centralized Authentication
* DNS
* Web Server
* Email Server
* TFTP Backup Server
* Extended ACLs
* Wireless Networking

The goal was not only to configure the network, but also to **verify connectivity, implement security policies, and simulate common enterprise networking and administration scenarios**.

---

# 🎯 Project Objectives

The main objectives of this project were to:

1. Design a scalable enterprise network topology using routers, switches, servers, wireless access points, and end devices.
2. Segment departments using VLANs to reduce broadcast traffic and improve security.
3. Implement inter-VLAN communication using Router-on-a-Stick.
4. Configure DHCP to automatically provide IP configuration to clients.
5. Implement dynamic routing using EIGRP.
6. Configure RSTP to prevent Layer 2 switching loops and provide fast convergence.
7. Secure network-device management using SSH and authentication mechanisms.
8. Implement centralized authentication using a RADIUS server.
9. Apply Extended ACLs to control access to critical network services.
10. Configure TFTP for network-device configuration backup and restoration.
11. Deploy enterprise services including DNS, Web, Mail, DHCP, AAA/RADIUS, and TFTP.

---

# 🏗️ Network Architecture

The network is divided into multiple departments using VLAN-based segmentation.

Each department is assigned its own IP subnet and default gateway.

### VLAN Design

| VLAN ID | Department  | Network          | Default Gateway |
| ------: | ----------- | ---------------- | --------------- |
|      10 | IT          | `192.168.1.0/24` | `192.168.1.1`   |
|      20 | Accounting  | `192.168.2.0/24` | `192.168.2.1`   |
|      30 | HR          | `192.168.3.0/24` | `192.168.3.1`   |
|      40 | Finance     | `192.168.4.0/24` | `192.168.4.1`   |
|      50 | Engineering | `192.168.5.0/24` | `192.168.5.1`   |
|      60 | Users       | `192.168.6.0/24` | `192.168.6.1`   |

The project also includes dedicated network segments for infrastructure and servers.

---

# 🔀 VLAN Segmentation

VLANs are used to logically separate different organizational departments.

### Department Segmentation

```text
                    Enterprise Network
                           |
        ┌──────────────────┴──────────────────┐
        │                                     │
      Switch 1                              Switch 2
        │                                     │
 ┌──────┼──────┐                       ┌──────┼──────┐
 │      │      │                       │      │      │
VLAN10 VLAN20 VLAN30                  VLAN40 VLAN50 VLAN60
 IT    Accounting HR                 Finance Eng.  Users
```

This segmentation provides:

* Logical separation between departments
* Smaller broadcast domains
* Improved network organization
* Better security and traffic control
* Easier network administration

---

# 🔗 Trunking & Router-on-a-Stick

Inter-VLAN routing is implemented using **Router-on-a-Stick (ROAS)**.

A single physical router interface is connected to the switch through an **IEEE 802.1Q trunk**.

The router then uses multiple subinterfaces, with each subinterface representing a VLAN and acting as that VLAN's default gateway.

### Conceptual Architecture

```text
                Router
                  |
            Physical Interface
                  |
          802.1Q Trunk Link
                  |
                Switch
        ┌─────────┼─────────┐
        │         │         │
      VLAN 10   VLAN 20   VLAN 30
        │         │         │
       IT     Accounting    HR
```

This allows devices in different VLANs to communicate through the router while maintaining logical segmentation.

---

# 🌐 Routing

The project uses both **Static Routing** and **EIGRP Dynamic Routing**.

## Static / Default Routing

Default routes are configured on selected routers to provide a **gateway of last resort** for unknown destinations.

## EIGRP

**Enhanced Interior Gateway Routing Protocol (EIGRP)** is used for dynamic route exchange between routers.

EIGRP allows routers to:

* Automatically exchange routing information
* Dynamically update routing tables
* Adapt to network changes
* Maintain connectivity between different network segments

### Routing Verification

Connectivity was tested from **VLAN 30** toward the remote network `10.10.50.4`.

The ping test was successful, confirming that the configured routing and inter-network communication were functioning correctly.

---

# 📡 DHCP

DHCP is implemented to automatically assign network configuration to end devices.

DHCP provides:

* IP Address
* Subnet Mask
* Default Gateway
* DNS Server Information

This eliminates the need for manually configuring every client and reduces administrative overhead.

### DHCP Networks

```text
VLAN 10 → 192.168.1.0/24
VLAN 20 → 192.168.2.0/24
VLAN 30 → 192.168.3.0/24
VLAN 40 → 192.168.4.0/24
VLAN 50 → 192.168.5.0/24
VLAN 60 → 192.168.6.0/24
```

DHCP Relay is also configured using `ip helper-address` to forward DHCP client requests toward the DHCP server where required.

---

# 🔄 Rapid Spanning Tree Protocol

**RSTP** is enabled on the switches to prevent Layer 2 switching loops.

It provides:

* Loop prevention
* Faster convergence
* Improved network stability
* Faster recovery from link failures

---

# 📶 Wireless Network

Wireless connectivity is integrated into the enterprise network through Access Points.

Two VLANs are extended through the wireless infrastructure.

### VLAN 30 — HR Wireless

* VLAN ID: `30`
* Department: HR
* 3 Laptops

### VLAN 60 — ITI Wireless

* VLAN ID: `60`
* SSID: `ITI`
* 1 Laptop
* 2 Smartphones

Wireless devices are mapped to their corresponding VLANs, allowing network access according to their assigned department.

---

# 🔐 Network Security

Security is implemented at multiple levels throughout the network.

## SSH Remote Management

Cisco routers and switches are configured for secure remote administration using **SSH**.

The configuration includes:

* Hostname configuration
* Domain name configuration
* Encrypted passwords
* Local user authentication
* RSA key generation
* SSH-only remote access

---

# 🛡️ AAA & RADIUS

The project implements **AAA (Authentication, Authorization, and Accounting)** using centralized authentication through a RADIUS server.

The authentication design uses two levels:

### Primary Authentication

```text
Administrator
     |
     | SSH
     ↓
Cisco Router / Switch
     |
     ↓
RADIUS Server
```

The network device first attempts to authenticate the administrator through the centralized RADIUS server.

### Local Fallback

If the RADIUS server becomes unavailable, the device falls back to its local user database.

This provides a backup authentication mechanism for administrative access.

---

# 🌍 Network Services

The enterprise environment contains several internal network services.

| Service      | IP Address     | Purpose                    |
| ------------ | -------------- | -------------------------- |
| DNS          | `192.168.7.10` | Hostname-to-IP resolution  |
| RADIUS / AAA | `192.168.7.20` | Centralized authentication |
| Web Server   | `10.10.50.4`   | Internal web services      |
| Mail Server  | `10.10.50.3`   | SMTP / POP3                |
| TFTP Server  | `10.10.50.2`   | Configuration backup       |

The DNS server acts as the central directory for resolving hostnames into IP addresses.

The TFTP server provides a centralized repository for network-device configuration backups.

The Mail Server provides organizational email services using SMTP and POP3.

---

# 🧱 Extended ACLs

Extended Access Control Lists are used to implement network security policies and control access to specific services.

The project demonstrates ACL filtering at different levels:

### 1. Host-Level DNS Restriction

Host:

```text
192.168.1.2
```

is prevented from accessing DNS over UDP port `53`.

Other hosts remain able to use the central DNS server.

---

### 2. Network-Level Web Restriction

The HR/Wireless network:

```text
192.168.3.0/24
```

is denied access to the internal Web Server:

```text
10.10.50.4
```

for:

```text
HTTP  → TCP/80
HTTPS → TCP/443
```

This demonstrates controlling access to services based on the source network.

---

### 3. VLAN-Level Mail Restriction

VLAN 10:

```text
192.168.1.0/24
```

is prevented from communicating with the central Mail Server:

```text
10.10.50.3
```

using:

```text
SMTP → TCP/25
POP3 → TCP/110
```

This demonstrates service-specific traffic filtering using Extended ACLs.

---

# 💾 TFTP Configuration Backup

A TFTP server is used as a centralized repository for Cisco device configurations.

This simulates an enterprise network maintenance scenario where device configurations can be:

* Backed up
* Restored
* Stored centrally
* Recovered after configuration changes or failures

---

# 🧪 Network Verification & Testing

The project includes multiple verification steps to confirm that the network operates as intended.

### Connectivity Testing

```text
VLAN 30
   |
   ↓
Router
   |
   ↓
Remote Network
10.10.50.4
   |
   ↓
PING SUCCESS
```

Routing was successfully verified through ICMP testing from VLAN 30 to the remote network.

Other areas verified during the project include:

* VLAN connectivity
* Inter-VLAN routing
* DHCP address assignment
* DHCP relay
* EIGRP routing
* SSH access
* RADIUS authentication
* Local authentication fallback
* DNS resolution
* Web access
* Mail services
* TFTP functionality
* ACL restrictions

---

# 🧰 Technologies & Protocols

| Category         | Technologies                       |
| ---------------- | ---------------------------------- |
| Switching        | VLAN, Trunking, RSTP               |
| Routing          | Static Routing, EIGRP              |
| Inter-VLAN       | Router-on-a-Stick                  |
| Addressing       | IPv4, DHCP                         |
| Wireless         | Access Points, VLAN-based Wireless |
| Security         | ACL, SSH, AAA                      |
| Authentication   | RADIUS                             |
| Network Services | DNS, Web, Mail, TFTP               |
| Management       | SSH, TFTP                          |
| Testing          | Ping / Connectivity Verification   |

---

# 📚 CCNA Concepts Demonstrated

This project provides hands-on implementation of the following CCNA topics:

```text
✓ VLANs
✓ VLAN Trunking
✓ 802.1Q
✓ Router-on-a-Stick
✓ Inter-VLAN Routing
✓ Static Routing
✓ EIGRP
✓ Default Routing
✓ DHCP
✓ DHCP Relay
✓ RSTP
✓ SSH
✓ RSA
✓ AAA
✓ RADIUS
✓ DNS
✓ HTTP/HTTPS
✓ SMTP/POP3
✓ TFTP
✓ Extended ACLs
✓ Wireless VLANs
✓ Network Troubleshooting
```

---

# 📁 Project Structure

A recommended GitHub repository structure:

```text
CCNA-Enterprise-Network/
│
├── README.md
│
├── Documentation/
│   └── CCNA_Project.pdf
│
├── Packet-Tracer/
│   └── Enterprise-Network.pkt
│
├── Configurations/
│   ├── Routers/
│   └── Switches/
│
├── Screenshots/
│   ├── Topology/
│   ├── VLAN/
│   ├── Routing/
│   ├── DHCP/
│   ├── SSH/
│   ├── AAA/
│   ├── ACL/
│   └── Services/
│
└── Verification/
    └── Test-Results.md
```

---

# 🚀 Key Learning Outcomes

Through this project, I gained practical experience in designing and configuring an enterprise network from the ground up.

### Networking

* Designing enterprise network topologies
* VLAN segmentation
* Trunk configuration
* Inter-VLAN routing
* Static and dynamic routing
* EIGRP implementation

### Network Services

* DHCP
* DHCP Relay
* DNS
* Web services
* Email services
* TFTP

### Security

* SSH hardening
* Local authentication
* Centralized RADIUS authentication
* AAA
* Extended ACLs
* Service-level traffic filtering

### Troubleshooting

* Connectivity testing
* Routing verification
* DHCP verification
* Authentication testing
* ACL validation
* Network-service verification

---

# 🎓 Project Purpose

This project was developed as a comprehensive **CCNA hands-on networking project** to bridge the gap between theoretical networking concepts and practical enterprise implementation.

Instead of implementing each CCNA topic independently, the project integrates multiple technologies into one interconnected infrastructure, providing practical experience with **network design, configuration, security, services, routing, and troubleshooting**.

---

# 👨‍💻 Author

**Abdelrahman Khaeld Elsayed**

CCNA / Network Infrastructure Project

---

# 📄 Documentation

The complete project documentation contains the detailed configuration and verification of the implemented enterprise network.

> **Note:** Credentials shown in the original lab documentation are for the simulated training environment only and should **not** be reused in production.
