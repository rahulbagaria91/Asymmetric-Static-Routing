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
