# 01 — Dual-ISP Enterprise WAN Redundancy

## Overview

This lab explores how an enterprise edge can maintain Internet reachability when its preferred ISP path becomes unavailable. The design uses two ISP paths and combines dynamic routing policy with reachability tracking.

**Environment:** Network simulation lab  
**Status:** Documentation started; topology screenshots, sanitized configurations, and captured verification outputs are still to be added.

## Problem statement

A single Internet exit creates a potential point of failure. The objective is to provide a preferred ISP path and an alternate path, then test failover and recovery when the preferred path loses reachability.

## Design objectives

1. Establish routing relationships with two ISP simulations.
2. Use OSPF for internal routing and iBGP between the enterprise edge routers.
3. Prefer ISP 1 for outbound path selection using a higher BGP Local Preference.
4. Use IP SLA and object tracking to monitor a target beyond the local interface.
5. Tie tracked static routing to reachability so a failed preferred path can be withdrawn from use.
6. Verify traffic uses the alternate ISP during failure and returns to the preferred path after recovery.
7. Apply outbound prefix filtering to avoid unintentionally feeding learned default routing information back toward an ISP.

## Technologies and design choices

| Technology | Purpose in this lab |
|---|---|
| eBGP | Exchange routing information between enterprise edge and ISP simulations |
| iBGP | Share BGP routing information between enterprise edge routers |
| OSPF | Provide internal reachability |
| BGP Local Preference | Prefer the primary ISP path within the enterprise AS |
| next-hop-self | Make an iBGP-learned path reachable through the advertising edge router when appropriate |
| IP SLA | Probe an external reachability target |
| Object tracking | Convert probe state into a trackable up/down condition |
| Tracked static route | Control route installation based on tracking state |
| Prefix filtering | Restrict which prefixes are advertised |

## High-level operation

- **Normal state:** The preferred ISP path is selected according to the configured routing policy.
- **Failure test:** The preferred path's monitored reachability is interrupted. The tracking state changes, and the dependent route is removed or no longer preferred as designed. Traffic should use the alternate path.
- **Recovery test:** Reachability returns, tracking recovers, and the primary path becomes available again. Confirm the intended policy selects it.

A physical interface failure and an upstream reachability failure are different test cases. Document which failure was introduced and what the routing protocols did in response.

## Verification checklist

Capture real outputs from the lab and place sanitized copies in an evidence/ folder.

- [ ] show ip interface brief — interface state and addressing
- [ ] show ip route — active routing table and default route
- [ ] show ip bgp summary — BGP neighbor state
- [ ] show ip bgp — BGP paths and path-selection attributes
- [ ] show ip protocols — routing protocol configuration/state
- [ ] show track — object tracking state
- [ ] show ip sla statistics — probe results
- [ ] show running-config | section ip sla
- [ ] show running-config | section track
- [ ] traceroute or sourced ping — forwarding path before, during, and after failure

Command availability and syntax can vary by Cisco IOS/IOSv image.

## Troubleshooting approach

| Symptom | Checks |
|---|---|
| BGP neighbor is not Established | Check peer addressing, reachability, remote AS, update source, and TCP/179 reachability |
| Primary route is not selected | Inspect received paths, Local Preference, next-hop reachability, and route policy |
| IP SLA probe fails continuously | Verify target, source interface/address, routing to target, and probe parameters |
| Track state does not follow the probe | Check the track-to-IP-SLA association and configured delay/threshold |
| Traffic does not fail over | Inspect tracked route, routing table, competing routes, and forwarding path |
| Traffic fails to return to primary | Check SLA recovery, track state, route reinstallation, and BGP best-path policy |

## Evidence and deliverables

Add these only after collecting them from the actual lab:

- topology/ — exported topology image
- configurations/ — sanitized router configurations
- evidence/ — normal, failure, and recovery command outputs
- troubleshooting/ — issue, investigation, root cause, and verified resolution

## What this project demonstrates

This lab is intended to demonstrate understanding of enterprise WAN resilience, BGP policy, route tracking, and systematic fault isolation. Discuss it as a simulation project, not as production operational experience.
