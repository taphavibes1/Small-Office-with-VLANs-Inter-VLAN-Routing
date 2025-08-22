# Small Office VLAN Segmentation (Cisco Packet Tracer)

## Project Overview
This project simulates a **small office network** where:
- Sales (VLAN 10) and HR (VLAN 20) should be isolated.
- Both departments need access to a **shared File Server** (VLAN 30).
- Implemented using **Router-on-a-Stick (Inter-VLAN Routing)**.

## Topology
- 1 Router (Router0)
- 1 Switch (Switch0)
- 4 PCs (2 Sales, 2 HR)
- 1 Server (File Server)

## VLAN & IP Scheme

| VLAN | Department | Network | Gateway |
|------|------------|---------|---------|
| 10   | Sales      | 192.168.10.0/24 | 192.168.10.1 |
| 20   | HR         | 192.168.20.0/24 | 192.168.20.1 |
| 30   | Server     | 192.168.30.0/24 | 192.168.30.1 |


## Configuration Highlights

### Switch

```bash
vlan 10
name Sales
vlan 20
name HR
vlan 30
name Server
!
int fa0/2
switchport mode access
switchport access vlan 10
interface fa0/3
switchport mode access
switchport access vlan 10
exit
interface fa0/4
switchport mode access
switchport access vlan 20
exit
interface fa0/5
switchport mode access
switchport access vlan 20
exit
interface fa0/6
switchport mode access
switchport access vlan 30
exit
! Set trunk link to router
interface fa0/1
switchport mode trunk
exit

```
### Router

```bash
enable
configure terminal
! Sub-interface for VLAN 10
interface fa0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
! Sub-interface for VLAN 20
interface fa0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
! Sub-interface for VLAN 30
interface fa0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit
! Enable physical interface
interface fa0/0
no shutdown
exit
```
