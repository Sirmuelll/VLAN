# VLAN
This repository contains a practical demonstration of VLAN (Virtual Local Area Network) configuration using Cisco devices. The project showcases how to segment a network into multiple isolated VLANs to enhance security, improve performance, and streamline management.
# VLAN Configuration Demo

## Overview
This project demonstrates the configuration of Virtual Local Area Networks (VLANs) to isolate and manage network traffic efficiently. The setup includes three departments: **Accounting**, **IT**, and **Sales**, each with dedicated VLANs. Specific communication rules are implemented:
- **Accounting** and **Sales** can communicate with each other.
- **IT** is isolated and cannot communicate with either **Accounting** or **Sales**.

This project highlights the use of VLANs to enhance network security and optimize traffic flow.

---

## Network Topology

### Components
1. **Accounting Department**:
   - **VLAN ID**: 10  
   - **Devices**: 3 computers  
   - Connected via a switch.

2. **IT Department**:
   - **VLAN ID**: 20  
   - **Devices**: 3 computers  
   - Connected via a switch.  
   - Fully isolated from other departments.

3. **Sales Department**:
   - **VLAN ID**: 30  
   - **Devices**: 3 computers and 1 wireless router.  
   - Connected via a switch.

---

### Communication Rules
| **Source VLAN** | **Destination VLAN** | **Communication** |
|-----------------|-----------------------|-------------------|
| VLAN 10 (Accounting) | VLAN 30 (Sales)       | Allowed           |
| VLAN 30 (Sales)      | VLAN 10 (Accounting)  | Allowed           |
| VLAN 10 (Accounting) | VLAN 20 (IT)          | Blocked           |
| VLAN 30 (Sales)      | VLAN 20 (IT)          | Blocked           |
| VLAN 20 (IT)         | VLAN 10 & 30          | Blocked           |

---

## Configuration Details

### VLAN IDs
- **VLAN 10**: Accounting  
- **VLAN 20**: IT  
- **VLAN 30**: Sales  

### Commands Used
Below are the key configuration commands applied to the switch:
```bash
# Create VLANs
vlan 10
 name Accounting
vlan 20
 name IT
vlan 30
 name Sales

# Assign ports to VLANs
interface range fastethernet 0/1-3
 switchport mode access
 switchport access vlan 10

interface range fastethernet 0/4-6
 switchport mode access
 switchport access vlan 20

interface range fastethernet 0/7-9
 switchport mode access
 switchport access vlan 30

# Configure trunk port for inter-switch communication
interface fastethernet 0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,30

#Verification Commands
# Check VLAN status
show vlan brief

# Check trunk port configuration
show interfaces trunk

# Verify VLAN assignment for ports
show running-config
