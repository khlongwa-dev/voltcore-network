# Runbook

## Opening the project

Open `configs/voltcore-network.pkt` in Cisco Packet Tracer. All four
core devices, `DBN-RTR`, `JHB-RTR`, `DBN-L3-SW`, `JHB-L3-SW`, are
pre-configured and should boot straight into a working state.

## Verifying VLANs

On either core switch:

```
  show vlan brief
  show ip interface brief
```

Confirms every VLAN is up and holding its assigned gateway address.

## Verifying routing

On either router:

```
  show ip route
```

Confirms static routes to every remote subnet are present and pointing
at the correct next hop.

## Verifying cross office connectivity

From a PC on any Durban VLAN, ping a device on any Johannesburg VLAN, and
the reverse. Both directions should succeed. If a ping fails, check the
static routes on both routers first, that is where a misconfiguration
here almost always shows up.

## Reproducing the config from scratch

The full running config for each device is in `configs/`, one file per
device. Paste the relevant file into a fresh device's CLI in config mode
to rebuild it from nothing.
