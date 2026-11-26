# 02 — Secure DMVPN Phase 2 Hub-and-Spoke VPN

## Overview

This lab explores a hub-and-spoke Dynamic Multipoint VPN design. Multipoint GRE provides a shared overlay interface, NHRP supports dynamic mapping and resolution of tunnel endpoints, and IPsec protects traffic across the underlay.

**Environment:** Network simulation lab  
**Status:** Documentation started; topology screenshots, sanitized configurations, and captured verification outputs are still to be added.

## Problem statement

Traditional point-to-point tunnel designs can require additional tunnel configuration as sites grow. DMVPN provides a scalable approach in which spokes register with a hub and can dynamically discover one another for direct spoke-to-spoke communication, subject to the Phase 2 design and routing behavior.

## Design objectives

1. Build a routed IP underlay between a hub and two spokes.
2. Configure a multipoint GRE overlay using a tunnel interface.
3. Use NHRP for dynamic tunnel endpoint registration and resolution.
4. Protect tunnel traffic with IKEv1 and IPsec.
5. Run OSPF over the tunnel overlay.
6. Verify hub-and-spoke adjacency and route exchange.
7. Generate spoke-to-spoke traffic and verify dynamic resolution and the forwarding path.

## Technologies and design choices

| Technology | Purpose |
|---|---|
| GRE / mGRE | Encapsulate overlay traffic; mGRE allows multiple tunnel peers on a multipoint interface |
| NHRP | Register and resolve tunnel protocol addresses to NBMA addresses |
| IKEv1 | Negotiate IPsec security associations and keying |
| IPsec ESP | Provide confidentiality and integrity protection according to the configured transform |
| OSPF | Exchange routes across the overlay |
| DMVPN Phase 2 | Support dynamic spoke-to-spoke tunnel formation while retaining hub-based control-plane roles |

The lab configuration uses IKEv1, pre-shared-key authentication, ESP, AES-256, SHA, and Diffie-Hellman Group 14. These are recorded as the parameters used in this lab, not as a recommendation for every modern deployment. For real deployments, select algorithms and IKE versions according to current organizational security policy and platform support.

## High-level operation

1. Each spoke reaches the hub's public/NBMA address through the routed underlay.
2. Spokes register their tunnel information with the hub using NHRP.
3. OSPF forms adjacencies across the overlay and advertises site routes.
4. When a spoke needs to communicate directly with another spoke, NHRP resolution supports discovery of the remote NBMA endpoint.
5. IPsec security associations protect the traffic as it crosses the underlay.

## Verification checklist

Capture real outputs from the lab and place sanitized copies in an evidence/ folder.

- [ ] show ip interface brief — physical and tunnel interface state
- [ ] show interface tunnel 0 — tunnel state and encapsulation details
- [ ] show ip nhrp — NHRP registrations and mappings
- [ ] show dmvpn — DMVPN peer/session information, if supported
- [ ] show crypto isakmp sa — IKEv1 security association state
- [ ] show crypto ipsec sa — IPsec security associations and packet counters
- [ ] show ip ospf neighbor — OSPF adjacency state
- [ ] show ip route ospf — routes learned through OSPF
- [ ] ping between hub and spokes, then between spokes
- [ ] traceroute and NHRP/IPsec counters during spoke-to-spoke traffic

Command availability and syntax can vary by Cisco IOS image and feature set.

## Troubleshooting approach

| Symptom | Checks |
|---|---|
| Tunnel interface is down | Check tunnel source/destination or mode, underlay reachability, and interface state |
| NHRP registration is missing | Check network ID, NHS configuration, tunnel addressing, and reachability to the hub |
| IKE SA does not establish | Check peer reachability, pre-shared-key consistency, IKE policy, and time/identity settings |
| IPsec counters do not increase | Check transform/protection configuration, crypto map or profile attachment, and interesting traffic |
| OSPF neighbor does not reach FULL | Check tunnel IP reachability, area/timers/authentication, network type, and MTU |
| Spoke-to-spoke traffic still uses the hub | Inspect NHRP resolution, routing next hop, Phase 2 behavior, and whether direct traffic has been triggered |

## Evidence and deliverables

Add these only after collecting them from the actual lab:

- topology/ — hub-and-spoke topology image
- configurations/ — sanitized hub and spoke configurations
- evidence/ — NHRP, DMVPN, IKE, IPsec, OSPF, ping, and traceroute outputs
- troubleshooting/ — issue, investigation, root cause, and verified resolution

Never publish pre-shared keys, passwords, private certificates, or other secrets. Replace them with clearly marked placeholders in shared configurations.

## What this project demonstrates

This lab is intended to demonstrate understanding of overlay/underlay separation, dynamic tunnel discovery, routing over VPN overlays, IPsec verification, and structured troubleshooting. It is a simulation project, not a production VPN deployment.
