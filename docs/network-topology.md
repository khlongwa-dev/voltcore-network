# Network Topology

## Durban HQ

Core switch `DBN-L3-SW` handles inter-VLAN routing and DHCP for the whole
site. Router `DBN-RTR` handles the WAN link out to Johannesburg.

| VLAN ID | Department | Subnet | Gateway |
|---|---|---|---|
| 10 | Management | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Executive | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Finance | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Engineering | 192.168.40.0/24 | 192.168.40.1 |
| 50 | IT | 192.168.50.0/24 | 192.168.50.1 |
| 60 | HR | 192.168.60.0/24 | 192.168.60.1 |
| 70 | Sales | 192.168.70.0/24 | 192.168.70.1 |
| 80 | Automation | 192.168.80.0/24 | 192.168.80.1 |

VLAN 10 has no DHCP pool, static addressing only, that's the servers and
core infrastructure VLAN. Every other VLAN gets a DHCP pool off the core
switch, with `192.168.10.10` set as the DNS server for all of them.

Core switch uplink to `DBN-RTR`: `Gi1/0/9`, routed port, `172.16.0.1/30`.
Seven trunk ports, `Gi1/0/2` through `Gi1/0/8`, one per access switch.

## Johannesburg Branch

Core switch `JHB-L3-SW` and router `JHB-RTR` follow the same pattern,
smaller scale.

| VLAN ID | Department | Subnet | Gateway |
|---|---|---|---|
| 10 | Management | 192.168.110.0/24 | 192.168.110.1 |
| 20 | IT | 192.168.120.0/24 | 192.168.120.1 |
| 30 | Automation | 192.168.130.0/24 | 192.168.130.1 |
| 40 | Field Ops | 192.168.140.0/24 | 192.168.140.1 |
| 50 | Sales | 192.168.150.0/24 | 192.168.150.1 |

Core switch uplink to `JHB-RTR`: `Gi1/0/6`, routed port, `172.16.1.1/30`.
DNS for every pool set to `192.168.110.10`.

## WAN Link

Point to point link between the two routers.

| Side | Interface | IP |
|---|---|---|
| DBN-RTR | Gi0/0/1 | 10.0.0.1/30 |
| JHB-RTR | Gi0/0/2 | 10.0.0.2/30 |

## Routing Design

Each core switch has a single default route pointing at its own router.
Each router carries explicit static routes to every subnet on the other
side, reached over the WAN link, plus explicit static routes back to its
own site's VLANs, reached through the core switch. Nothing relies on a
routing protocol, every path is deliberate and traceable.

Cross office ping confirmed working between both LANs.
