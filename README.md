# [Failover Network Using Redundant Paths](https://github.com/Istiaq-Alam/Failover-Network-Using-Redundant-Paths.git)🔗

This project demonstrates how to build a **highly available and resilient network** by implementing **Spanning Tree Protocol (STP)** and **Hot Standby Router Protocol (HSRP)** for single backup router & **MHSRP** for multiple backup router. The goal is to prevent network failures, loops, and downtime in mission-critical environments such as hospitals, banks, and universities.

## 📌 Problem Statement

In critical networks, even a **single point of failure**—such as a device or link going down—can cause complete network outages. Simply adding redundant physical paths without proper control protocols may result in:

- Network loops
- Broadcast storms
- Service disruption
- Data inaccessibility

## ✅ Solution Overview

This project applies two key protocols to manage redundancy effectively:

### 🔁 Spanning Tree Protocol (STP)
- STP blocks redundant links during normal operations to prevent loops.
- Automatically unblocks backup links when a primary link fails.
- Ensures a loop-free, self-healing Layer 2 topology.

### 🛡️ Hot Standby Router Protocol (HSRP)
- Configures two routers to share a **virtual IP address**.
- One router acts as **Active**, the other as **Standby**.
- Automatically fails over to the standby router if the active one fails.
- Ensures uninterrupted gateway availability at Layer 3.

## 🎯 Expected Outcomes

- **High Availability**: Network remains operational despite failures.
- **Automatic Failover**: Traffic is rerouted seamlessly.
- **Increased Reliability**: Essential for organizations where uptime is critical.

## 📂 Project Files

- **Network Diagrams** – Show topology with redundant paths.
- **Configurations** – STP and HSRP implementation details.
- **Simulation/Packet Tracer Files** – Demonstration of failover in action.

## 🧑‍💻 Tools Used

- Cisco Packet Tracer (or equivalent simulator)
- Cisco IOS commands
- Basic networking hardware concepts

## 🧠 Learning Objectives

- Understand Layer 2 and Layer 3 failover mechanisms.
- Implement STP and HSRP in a simulated environment.
- Improve fault tolerance in enterprise-level networks.

## 📅 Presented On

**Computer Network Course**  
**June 16, 2025**

---

Feel free to fork, clone, or contribute to this project!
