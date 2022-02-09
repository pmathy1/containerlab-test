# AVD_FABRIC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| AVD_FABRIC | l3leaf | AVD-LEAF1 | 172.20.20.6/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | AVD-LEAF2 | 172.20.20.8/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | AVD-LEAF3 | 172.20.20.3/24 | cEOS | Provisioned |
| AVD_FABRIC | l3leaf | AVD-LEAF4 | 172.20.20.4/24 | cEOS | Provisioned |
| AVD_FABRIC | spine | AVD-SPINE1 | 172.20.20.2/24 | cEOS | Provisioned |
| AVD_FABRIC | spine | AVD-SPINE2 | 172.20.20.5/24 | cEOS | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | AVD-LEAF1 | Ethernet1 | spine | AVD-SPINE1 | Ethernet1 |
| l3leaf | AVD-LEAF1 | Ethernet2 | spine | AVD-SPINE2 | Ethernet1 |
| l3leaf | AVD-LEAF1 | Ethernet3 | mlag_peer | AVD-LEAF2 | Ethernet3 |
| l3leaf | AVD-LEAF2 | Ethernet1 | spine | AVD-SPINE1 | Ethernet2 |
| l3leaf | AVD-LEAF2 | Ethernet2 | spine | AVD-SPINE2 | Ethernet2 |
| l3leaf | AVD-LEAF3 | Ethernet1 | spine | AVD-SPINE1 | Ethernet3 |
| l3leaf | AVD-LEAF3 | Ethernet2 | spine | AVD-SPINE2 | Ethernet3 |
| l3leaf | AVD-LEAF3 | Ethernet3 | mlag_peer | AVD-LEAF4 | Ethernet3 |
| l3leaf | AVD-LEAF4 | Ethernet1 | spine | AVD-SPINE1 | Ethernet4 |
| l3leaf | AVD-LEAF4 | Ethernet2 | spine | AVD-SPINE2 | Ethernet4 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 16 | 6.25 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| AVD-LEAF1 | Ethernet1 | 172.31.255.1/31 | AVD-SPINE1 | Ethernet1 | 172.31.255.0/31 |
| AVD-LEAF1 | Ethernet2 | 172.31.255.3/31 | AVD-SPINE2 | Ethernet1 | 172.31.255.2/31 |
| AVD-LEAF2 | Ethernet1 | 172.31.255.5/31 | AVD-SPINE1 | Ethernet2 | 172.31.255.4/31 |
| AVD-LEAF2 | Ethernet2 | 172.31.255.7/31 | AVD-SPINE2 | Ethernet2 | 172.31.255.6/31 |
| AVD-LEAF3 | Ethernet1 | 172.31.255.9/31 | AVD-SPINE1 | Ethernet3 | 172.31.255.8/31 |
| AVD-LEAF3 | Ethernet2 | 172.31.255.11/31 | AVD-SPINE2 | Ethernet3 | 172.31.255.10/31 |
| AVD-LEAF4 | Ethernet1 | 172.31.255.13/31 | AVD-SPINE1 | Ethernet4 | 172.31.255.12/31 |
| AVD-LEAF4 | Ethernet2 | 172.31.255.15/31 | AVD-SPINE2 | Ethernet4 | 172.31.255.14/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 6 | 2.35 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | AVD-LEAF1 | 192.168.255.3/32 |
| AVD_FABRIC | AVD-LEAF2 | 192.168.255.4/32 |
| AVD_FABRIC | AVD-LEAF3 | 192.168.255.5/32 |
| AVD_FABRIC | AVD-LEAF4 | 192.168.255.6/32 |
| AVD_FABRIC | AVD-SPINE1 | 192.168.255.1/32 |
| AVD_FABRIC | AVD-SPINE2 | 192.168.255.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.254.0/24 | 256 | 4 | 1.57 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| AVD_FABRIC | AVD-LEAF1 | 192.168.254.3/32 |
| AVD_FABRIC | AVD-LEAF2 | 192.168.254.3/32 |
| AVD_FABRIC | AVD-LEAF3 | 192.168.254.5/32 |
| AVD_FABRIC | AVD-LEAF4 | 192.168.254.5/32 |
