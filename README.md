# 🔀 Asymmetric Static Routing | Cisco CCNA Lab

> A hands-on Cisco networking lab demonstrating **Asymmetric Static Routing** using six Cisco 2911 routers, two LANs, and multiple routed paths.

---

## 📌 Project Overview

This lab demonstrates how **static routes** can be configured to intentionally use different paths for forward and return traffic.

The network consists of **6 Cisco 2911 routers connected in a ring topology**. Static routing is configured so that traffic between the two LANs follows different paths in each direction.

### Forward Traffic

```text
PC0
 │
 ▼
SW1
 │
 ▼
R1 → R2 → R3 → R4
                    │
                    ▼
                   SW2
                    │
                    ▼
                   PC2




🎯 Objectives

The main objectives of this lab were:

Understand static routing
Configure Cisco router interfaces
Configure IPv4 addressing
Configure next-hop static routes
Understand routing table entries
Implement asymmetric traffic paths
Verify routing decisions
Test end-to-end connectivity
Use ping and tracert for troubleshooting
Gain practical Cisco IOS experience
🏗️ Network Topology

Topology Summary
Device	Role
R1	Edge Router / LAN Gateway
R2	Transit Router
R3	Transit Router
R4	Edge Router / LAN Gateway
R5	Alternate Return Path
R6	Alternate Return Path
SW1	Left LAN Switch
SW2	Right LAN Switch
PC0, PC1	Left LAN Hosts
PC2, PC3	Right LAN Hosts
🌐 IP Addressing Plan
LAN Networks
Network	Device	Interface	IP Address
192.168.10.0/24	R1	G0/0	192.168.10.1
192.168.10.0/24	PC0	NIC	192.168.10.10
192.168.10.0/24	PC1	NIC	192.168.10.11
192.168.20.0/24	R4	G0/0	192.168.20.1
192.168.20.0/24	PC2	NIC	192.168.20.10
192.168.20.0/24	PC3	NIC	192.168.20.11
Router-to-Router Networks
Link	Network	Device A	Device B
R1 ↔ R2	10.0.20.0/24	R1 G0/1 – 10.0.20.1	R2 G0/1 – 10.0.20.2
R2 ↔ R3	10.0.30.0/24	R2 G0/2 – 10.0.30.1	R3 G0/1 – 10.0.30.2
R3 ↔ R4	10.0.40.0/24	R3 G0/2 – 10.0.40.1	R4 G0/1 – 10.0.40.2
R4 ↔ R5	10.0.50.0/24	R4 G0/2 – 10.0.50.1	R5 G0/2 – 10.0.50.2
R5 ↔ R6	10.0.60.0/24	R5 G0/1 – 10.0.60.1	R6 G0/1 – 10.0.60.2
R6 ↔ R1	10.0.70.0/24	R6 G0/2 – 10.0.70.1	R1 G0/2 – 10.0.70.2
🔀 Routing Design

The network was designed with two different paths between the LANs.

➡️ Forward Path
192.168.10.0/24
      ↓
     R1
      ↓
     R2
      ↓
     R3
      ↓
     R4
      ↓
192.168.20.0/24
⬅️ Return Path
192.168.20.0/24
      ↓
     R4
      ↓
     R5
      ↓
     R6
      ↓
     R1
      ↓
192.168.10.0/24

This demonstrates how static routes can control the forwarding path in each direction.

⚙️ Static Routing Configuration
R1
ip route 192.168.20.0 255.255.255.0 10.0.20.2
R2
ip route 192.168.20.0 255.255.255.0 10.0.30.2
R3
ip route 192.168.10.0 255.255.255.0 10.0.40.2
R4
ip route 192.168.10.0 255.255.255.0 10.0.50.2
R5
ip route 192.168.10.0 255.255.255.0 10.0.60.2
R6
ip route 192.168.10.0 255.255.255.0 10.0.70.2
🖥️ Router Configuration

The router interfaces were configured with IPv4 addresses and enabled using:

interface gigabitEthernet 0/0
ip address <IP_ADDRESS> <SUBNET_MASK>
no shutdown

The same configuration approach was applied to the required router interfaces.

📋 Routing Table Verification

Static routes were verified using:

show ip route

For example, R1 contains:

S 192.168.20.0/24 [1/0] via 10.0.20.2

The S indicates a static route, while [1/0] represents the administrative distance and metric.

🧪 Connectivity Testing
Forward Connectivity

PC0 was used to test connectivity toward PC2:

PC0 → PC1 LAN → R1 → R2 → R3 → R4 → PC2

Test command:

ping 192.168.20.10

Return Connectivity

PC2 was then used to test connectivity toward PC0:

PC2 → R4 → R5 → R6 → R1 → PC0

Test command:

ping 192.168.10.10

🔎 Path Verification

Traceroute was used to observe the path taken by packets.

Forward Path
PC0 → R1 → R2 → R3 → R4 → PC2

Command:

tracert 192.168.20.10

Return Path
PC2 → R4 → R5 → R6 → R1 → PC0

Command:

tracert 192.168.10.10

🛠️ Verification Commands

Some useful Cisco IOS commands used in this lab:

show ip interface brief

Check interface status and IP addresses.

show ip route

Display the routing table.

show ip route static

Display static routes.

show running-config

Display the active configuration.

ping <destination-ip>

Test Layer 3 connectivity.

🧠 Key Concepts Practiced
IPv4 Addressing
Subnet Masks
Cisco IOS
Router Interface Configuration
Static Routing
Next-Hop Routing
Routing Tables
Packet Forwarding
Asymmetric Routing
Network Troubleshooting
Ping
Traceroute
Cisco Packet Tracer
💻 Tools & Technologies
Cisco Packet Tracer
Cisco IOS
Cisco 2911 Routers
Cisco 2960 Switches
IPv4
Static Routing
📁 Project Files
Asymmetric-Static-Routing/
│
├── README.md
├── topology.png
│
├── 01-R1-Configuration.png
├── 02-Routing-Table.png
├── 03-PC0-to-PC2-Ping.png
├── 04-PC2-to-PC0-Ping.png
├── 05-Forward-Tracert.png
├── 06-Return-Tracert.png
│
└── Asymmetric-Static-Routing.pkt
📚 Learning Outcome

This lab provided practical experience with configuring and troubleshooting a multi-router Cisco network.

The main takeaway was understanding how static routes and next-hop addresses influence packet forwarding, and how different routes can be used for forward and return traffic.

🚀 Future Improvements

Possible extensions of this lab:

Replace static routing with OSPF
Configure floating static routes
Simulate router/link failure
Compare static routing with dynamic routing
Configure routing redundancy
Analyze convergence behavior
Perform additional troubleshooting scenarios
👨‍💻 Author

Rahul Bagaria

B.Tech — Computer Science & Engineering

Areas of Interest
🌐 Networking
🔐 Cybersecurity
🛡️ SOC Operations
📡 Network Security
🖥️ Cisco Networking
🔎 Network Troubleshooting

⭐ This project is part of my CCNA hands-on learning and networking lab practice.

#CCNA #Cisco #Networking #CiscoPacketTracer #StaticRouting #Routing #NetworkEngineering #CiscoIOS #NetworkingLab #ComputerNetworking
