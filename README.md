# Virtual-Lab-ICS-Segmentation
This lab demonstrates how to design, deploy, and secure a multi‑zone industrial environment using VirtualBox and OPNsense. It includes four isolated security zones (LAN, SCADA, PLC, DMZ), aligned with ISA/IEC 62443 and the Purdue Enterprise Reference Architecture.

The project provides hands‑on experience with:  
• IT/OT segmentation and firewall rule engineering  
• SCADA → PLC communication flows  
• ICS protocol analysis (Modbus TCP, PROFINET, S7comm)  
• Wireshark dissectors for industrial traffic  
• DMZ design for historians and jump hosts  
• Testing and validating segmentation boundaries  

This lab is intended for OT/ICS security learners, network engineers, and cybersecurity professionals who want to practice industrial network design, protocol analysis, and secure architecture concepts in a safe virtual environment.




# 🏭 Virtual ICS/OT Security Lab  
### IT/OT Segmentation • Purdue Model • ICS Protocols • OPNsense Firewall

This repository contains a fully virtualized **Industrial Control System (ICS) / Operational Technology (OT)** security lab built using **VirtualBox** and **OPNsense**.  
It is designed for hands‑on learning of:

- Industrial network segmentation  
- ICS protocols (Modbus, PROFINET, S7comm, CIP)  
- Purdue Model architecture  
- ISA/IEC 62443 security concepts  
- Firewall rule design for OT environments  

This lab mirrors the architecture used in **real factories, power plants, and industrial automation networks**.

---

# Objectives

## **A) IT/OT Segmentation**
Implement a 4‑zone industrial network:

| Zone | Interface | Network | Purpose |
|------|-----------|---------|---------|
| **LAN (IT)** | em0 | 192.168.1.0/24 | Engineering workstation, IT tools |
| **SCADA** | em1 | 192.168.20.0/24 | HMI, SCADA servers |
| **PLC** | em2 | 192.168.30.0/24 | PLCs, controllers |
| **DMZ** | em3 | 192.168.40.0/24 | Historian, jump host |

Segmentation follows **ISA/IEC 62443** and the **Purdue Model**.

---

# 🧱 Architecture Overview

## **Network Topology Diagram**
+---------------------------+
|        IT LAN (L4)        |
| 192.168.1.0/24            |
+-------------+-------------+
|
| Allow IT → SCADA
v
+---------------------------------------------------------------+
|                         OPNsense Firewall                     |
|                                                               |
|  LAN (em0)   SCADA (em1)   PLC (em2)     DMZ (em3)            |
| 1.1          20.1          30.1          40.1                 |
|                                                               |
|  - Block IT → PLC                                             |
|  - Allow SCADA → PLC                                          |
|  - Block SCADA → Internet                                     |
|  - Optional DMZ rules                                         |
+---------------------------------------------------------------+
|
| Controlled conduits
v
+---------------------------+
|     SCADA / PLC Zones     |
+---------------------------+

---

# 🏛 Purdue Model Mapping

## **Purdue Model Diagram**

+-------------------------------------------------------------+
| Level 5 — Enterprise Network (Corporate IT)                 |
+-------------------------------------------------------------+
| Level 4 — Site Business Network (IT LAN)                    |
|   • Windows workstation                                      |
|   • Active Directory (optional)                              |
+-------------------------------------------------------------+
| Level 3 — Operations / SCADA                                |
|   • SCADA VM (HMI, SCADA server)                             |
+-------------------------------------------------------------+
| Level 3.5 — Industrial DMZ                                  |
|   • Historian                                                |
|   • Jump host                                                |
+-------------------------------------------------------------+
| Level 2 — Control Network                                   |
|   • PLC simulators                                           |
|   • Modbus/PROFINET devices                                  |
+-------------------------------------------------------------+
| Level 1 — Field Devices                                     |
|   • Sensors, actuators (simulated)                           |
+-------------------------------------------------------------+


---

# 🔥 Firewall Rules Implemented

### **LAN → SCADA**
✔ Allowed  
Used for engineering workstation access.

### **LAN → PLC**
❌ Blocked  
Critical OT security requirement.

### **SCADA → PLC**
✔ Allowed  
Required for control traffic (Modbus, PROFINET, CIP).

### **SCADA → Internet**
❌ Blocked  
62443 requirement.

### **DMZ ↔ SCADA**
✔ Allowed (limited)  
Historian / jump host communication.

---

# 🖥 Virtual Machines

### **1. OPNsense Firewall**
- 4 NICs mapped to 4 internal networks  
- Implements segmentation and traffic control  

### **2. IT Workstation (LAN)**
- Windows 10/11  
- Used for testing and engineering access  

### **3. SCADA VM**
- Windows or Linux  
- Runs HMI, SCADA tools, Modbus master, Wireshark  

### **4. PLC VM**
- OpenPLC or Modbus simulator  
- Represents Level 2 controllers  

### **5. DMZ VM**
- Historian, jump host, or logging server  

---

# 🧪 Testing Performed

### ✔ LAN → SCADA ping  
### ✔ LAN → PLC blocked  
### ✔ LAN → DMZ blocked  
### ✔ SCADA → PLC (after SCADA VM is installed)  
### ✔ SCADA → Internet blocked  
### ✔ Firewall logs validated  

---

# 📚 Skills Practiced

- ICS/OT network design  
- ISA/IEC 62443 segmentation  
- Purdue Model architecture  
- Firewall rule design  
- ICS protocol analysis  
- Virtualized industrial environments  
- Threat modeling for OT  

---

# 🚀 Next Steps

- Install SCADA VM  
- Install PLC simulator  
- Capture Modbus/PROFINET traffic  
- Build historian in DMZ  
- Add Active Directory to IT LAN  
- Add intrusion detection (Suricata/Snort)  

---

# 🏁 Summary

This lab replicates a **real industrial network** with proper segmentation, ICS protocol support, and security controls.  
It is suitable for:

- OT security learning  
- ICS protocol analysis  
- SOC/Blue Team practice  
- Industrial network engineering  
- Cyber‑range training  
