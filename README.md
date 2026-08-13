# Voltcore Network

## WAN and VLAN Infrastructure — Phase 3 Project

A full scale simulation of Voltcore Engineering Solutions' two office
network, built in Cisco Packet Tracer. Same fictional company running
through the rest of this roadmap, Durban HQ and a Johannesburg Branch,
now connected end to end over a WAN link with full inter office routing.

## Overview

- **Durban HQ**, primary site, 1 router, 1 Layer 3 core switch, 7 Layer 2
  access switches, 66 devices, 8 VLANs
- **Johannesburg Branch**, secondary site, 1 router, 1 Layer 3 core switch,
  4 Layer 2 access switches, 28 devices, 5 VLANs
- WAN link joining both sites, static routing on every hop, cross office
  ping confirmed working

Full VLAN and IP breakdown is in `docs/network-topology.md`.

## Repository Structure

```text
voltcore-network/
├── configs/
│   ├── voltcore-network.pkt
│   ├── dbn-rtr-config.txt
│   ├── jhb-rtr-config.txt
│   ├── dbn-core-switch-config.txt
│   └── jhb-core-switch-config.txt
├── docs/
│   ├── network-topology.md
│   └── screenshots/
├── README.md
└── RUNBOOK.md
```

---

## What's Next

VPN tunneling between the two offices, so traffic across the WAN link is
encrypted rather than sent in the clear. That is the next piece of this
phase.

---

## Part of a Larger Journey

This project is Phase 3 of a personal 110 day Systems Administration
roadmap. Phase 1 was a hardened Linux server. Phase 2 was a full Active
Directory environment for the same fictional company. Phase 4 is
Coredesk, an IT helpdesk platform running on top of all of it.

Every phase is documented publicly as it is completed.
