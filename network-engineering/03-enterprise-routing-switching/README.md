# 03 — Enterprise Routing & Switching Labs

## Overview

A set of enterprise campus and routing exercises covering Layer 2 segmentation, loop prevention, link aggregation, and dynamic routing.

**Environment:** GNS3 and Cisco Packet Tracer  
**Status:** Documentation started; topology screenshots, sanitized configurations, and captured verification outputs are still to be added.

## Lab objectives

### Layer 2 switching

- Create and verify VLANs.
- Configure access ports and 802.1Q trunks.
- Implement inter-VLAN routing.
- Understand and verify STP, RSTP, PVST+, and Rapid PVST+ behavior.
- Configure EtherChannel using LACP and PAgP.
- Practice switch security controls such as port security, DHCP snooping, and Dynamic ARP Inspection where supported.

### Layer 3 routing

- Configure single-area and multi-area OSPF.
- Practice OSPF area types, including stub, totally stubby, and NSSA behavior.
- Inspect OSPF neighbor states, LSAs, route types, and route summarization.
- Configure EIGRP and inspect successor/feasible successor behavior where applicable.
- Practice BGP peering and path selection using attributes such as Weight, Local Preference, and AS-path prepending.
- Practice static and floating static routes, redistribution, route filtering, and route maps.

## Why these technologies matter

| Technology | Operational purpose |
|---|---|
| VLANs | Separate Layer 2 broadcast domains |
| Trunking | Carry multiple VLANs between network devices |
| Inter-VLAN routing | Enable Layer 3 communication between VLANs |
| STP / RSTP | Prevent Layer 2 loops while providing redundant paths |
| EtherChannel | Combine physical links into a logical bundle |
| OSPF | Provide link-state dynamic routing within an autonomous system |
| EIGRP | Provide dynamic routing using a composite metric and DUAL |
| BGP | Exchange routing information between autonomous systems and apply routing policy |
| ACLs / prefix lists / route maps | Control traffic or route advertisement/selection according to policy |

## Verification checklist

Capture real outputs from the lab and place sanitized copies in an evidence/ folder.

**Switching**
- [ ] show vlan brief
- [ ] show interfaces trunk
- [ ] show spanning-tree
- [ ] show etherchannel summary
- [ ] show interfaces status
- [ ] show port-security interface

**Routing**
- [ ] show ip interface brief
- [ ] show ip route
- [ ] show ip ospf neighbor
- [ ] show ip ospf database
- [ ] show ip eigrp neighbors (where supported)
- [ ] show ip eigrp topology (where supported)
- [ ] show ip bgp summary
- [ ] show ip bgp
- [ ] show access-lists

Use commands supported by the specific IOS image and feature set in the lab.

## Troubleshooting workflow

1. **Physical layer:** Verify power, cabling, interface state, speed, and duplex.
2. **Layer 2:** Check VLAN membership, trunk allowed/native VLANs, STP state, and EtherChannel consistency.
3. **Layer 3:** Check IP addressing, masks, connected routes, and next-hop reachability.
4. **Routing protocol:** Check neighbor state, timers, area/AS parameters, authentication, and advertised networks.
5. **Route selection:** Inspect the routing table and protocol-specific path attributes/metrics.
6. **Forwarding:** Use ping and traceroute, then inspect ACLs and relevant counters.

## Evidence and deliverables

Add these only after collecting them from the actual lab:

- topology/ — topology diagrams or exported screenshots
- configurations/ — sanitized device configurations grouped by lab
- evidence/ — command outputs that demonstrate the actual state
- troubleshooting/ — symptom, commands used, findings, root cause, and verified fix

## What this project demonstrates

These exercises are intended to demonstrate practical familiarity with campus switching, routing protocols, path selection, redundancy, and methodical troubleshooting. Describe them as hands-on lab work, not professional production experience.
