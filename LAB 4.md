# Lab 02 — Unknown MAC Address and MAC Learning

## Objective

Demonstrate how a Cisco switch behaves when the destination MAC address is not yet present in its MAC address table, and observe how the switch dynamically learns MAC addresses from network traffic.

## Topology

Seven PCs were connected to one Cisco switch.

```text
                         ┌── PC0
                         │
                         ├── PC1
                         │
                         ├── PC2
                         │
PCs ───────────────── Switch0
                         ├── PC4
                         │
                         ├── PC5
                         │
                         ├── PC6
                         │
                         └── PC7
```

### Physical Connections

| Device | Switch Port | Cable                   |
| ------ | ----------- | ----------------------- |
| PC0    | Fa0/1       | Copper Straight-Through |
| PC1    | Fa0/2       | Copper Straight-Through |
| PC2    | Fa0/3       | Copper Straight-Through |
| PC3    | Fa0/4       | Copper Straight-Through |
| PC4    | Fa0/5       | Copper Straight-Through |
| PC5    | Fa0/6       | Copper Straight-Through |
| PC6    | Fa0/7       | Copper Straight-Through |
| PC7    | Fa0/8       | Copper Straight-Through |

## IP Addressing

All PCs were configured on the same IPv4 network.

| Device | IPv4 Address   | Subnet Mask     |
| ------ | -------------- | --------------- |
| PC0    | `192.168.1.10` | `255.255.255.0` |
| PC1    | `192.168.1.20` | `255.255.255.0` |
| PC2    | `192.168.1.30` | `255.255.255.0` |
| PC3    | `192.168.1.40` | `255.255.255.0` |
| PC4    | `192.168.1.50` | `255.255.255.0` |
| PC5    | `192.168.1.60` | `255.255.255.0` |
| PC6    | `192.168.1.70` | `255.255.255.0` |
| PC7    | `192.168.1.80` | `255.255.255.0` |

Default gateway was not required because all devices were communicating within the same `192.168.1.0/24` network.

## Initial MAC Address Table

After connecting the PCs and allowing the topology to operate, the switch was inspected using:

```text
enable
show mac address-table
```

The switch displayed dynamically learned MAC addresses:

```text
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0001.434d.0458    DYNAMIC     Fa0/4
   1    0001.637b.9b41    DYNAMIC     Fa0/3
   1    0001.9787.1c53    DYNAMIC     Fa0/2
   1    0007.ecad.2a5a    DYNAMIC     Fa0/7
   1    0060.3e1a.c157    DYNAMIC     Fa0/6
   1    0060.3e8c.616e    DYNAMIC     Fa0/8
   1    0090.2196.6dc5    DYNAMIC     Fa0/5
```

The entries were marked **DYNAMIC**, meaning that the switch learned them automatically from Ethernet traffic.

## Challenge Encountered

The initial objective was to demonstrate what happens when a switch receives a frame whose destination MAC address is unknown.

However, when traffic was initially sent from **PC0 to PC7**, the switch already had MAC addresses learned in its MAC address table.

Therefore, the switch was able to identify the appropriate port instead of demonstrating the unknown-destination behavior I was trying to observe.

This created an important practical question:

> **How did the switch already know the MAC addresses in a newly created topology?**

The investigation showed that switches learn MAC addresses automatically by examining the **source MAC address of incoming Ethernet frames**.

## Clearing the Dynamic MAC Table

To restart the experiment with the dynamically learned MAC entries removed, the switch was first placed into privileged EXEC mode.

The first attempt was made from User EXEC mode:

```text
Switch> clear mac address-table dynamic
```

This produced:

```text
% Invalid input detected at '^' marker.
```

The reason was that the command requires privileged EXEC mode.

The correct procedure was:

```text
Switch> enable
Switch# clear mac address-table dynamic
```

The MAC table was then checked with:

```text
Switch# show mac address-table
```

This allowed the experiment to be repeated without relying on the previously learned dynamic MAC entries.

## Unknown Destination Experiment

After clearing the dynamically learned MAC addresses, traffic was generated from:

```text
PC0 → PC7
```

PC0:

```text
192.168.1.10
```

PC7:

```text
192.168.1.80
```

At this stage, the switch did not yet have the required destination MAC-to-port mapping.

Because the switch could not identify a specific outgoing port for the destination MAC, the frame was flooded within the VLAN rather than being immediately forwarded to one known destination port.

This behavior demonstrated the difference between **unknown unicast forwarding** and **known unicast forwarding**.

## MAC Learning Process

The switch learns MAC addresses from the source address of incoming Ethernet frames.

For example:

```text
PC7 → Switch0
```

The switch examines the source MAC address of the frame and associates it with the port through which the frame arrived.

Conceptually:

```text
PC7 MAC → Fa0/8
```

The switch stores this information in its MAC address table.

The entry is marked:

```text
DYNAMIC
```

because it was learned automatically rather than manually configured.

## Known Destination Test

After the switch had learned the relevant MAC address, the same communication was tested again:

```text
PC0 → PC7
```

The switch could now use its MAC address table to identify the appropriate outgoing interface.

The forwarding process therefore changed from:

```text
Unknown destination
        ↓
Switch does not know destination port
        ↓
Frame is flooded within the VLAN
```

to:

```text
Known destination
        ↓
Switch checks MAC address table
        ↓
Destination MAC mapped to a port
        ↓
Frame forwarded toward the appropriate port
```

## CLI Commands Used

### Enter privileged EXEC mode

```text
Switch> enable
```

### Display MAC address table

```text
Switch# show mac address-table
```

### Clear dynamically learned MAC addresses

```text
Switch# clear mac address-table dynamic
```

### Verify the MAC address table again

```text
Switch# show mac address-table
```

## Important Concept — MAC Learning

A switch does **not** normally learn a MAC address because that MAC appears as the destination.

It learns the address from the **source MAC address** of an incoming frame.

Example:

```text
PC7
  │
  │ Source MAC = PC7's MAC
  ▼
Switch0
  │
  └── Learns: PC7 MAC → Fa0/8
```

This allows the switch to build its MAC address table automatically.

## Unknown vs Known Unicast

### Unknown destination

```text
PC0 → Switch
          ├── PC1
          ├── PC2
          ├── PC3
          ├── PC4
          ├── PC5
          ├── PC6
          └── PC7
```

The switch does not know the destination port, so the frame is flooded within the VLAN.

### Known destination

```text
PC0 → Switch → PC7
```

The switch has learned the destination MAC and associated it with the appropriate port.

## What I Learned

* Switches dynamically learn MAC addresses.
* The MAC address table maps MAC addresses to switch interfaces.
* `DYNAMIC` entries are learned automatically.
* A switch learns from the source MAC address of incoming frames.
* An unknown destination MAC can cause a frame to be flooded within the VLAN.
* Once the destination MAC is learned, subsequent traffic can be forwarded through the appropriate port.
* Clearing the dynamic MAC table is useful when testing the learning process from the beginning.
* CLI output provides evidence of what the switch has actually learned instead of relying only on Packet Tracer animation.

## Cybersecurity Connection

Understanding MAC learning and forwarding is important for cybersecurity because Layer 2 behavior forms the foundation for:

* Network traffic analysis
* ARP security
* MAC address analysis
* Network monitoring
* Switch security
* Detection of abnormal Layer 2 behavior
* Understanding network reconnaissance
* Investigating attacks involving Ethernet and MAC addresses

## Evidence

The recorded Packet Tracer video documents the experiment, including the unknown-destination forwarding behavior and subsequent MAC learning.

The `.pkt` file should also be retained so that the topology and experiment can be reopened and reproduced in Cisco Packet Tracer.

## Conclusion

This experiment demonstrated how a switch transitions from not knowing a destination's location to learning its MAC address and subsequently using that information for targeted forwarding. 
## Click the Thumbnail Below to View My YouTube Video

[![Unknown Unicast Flooding & MAC Learning](https://img.youtube.com/vi/PuRQQB0d8tg/maxresdefault.jpg)](https://www.youtube.com/watch?v=PuRQQB0d8tg)

 
The most important principle demonstrated was:

```text
Learn source MAC
       ↓
Associate MAC with incoming port
       ↓
Store entry in MAC address table
       ↓
Use table for future forwarding decisions
```

**Lab principle:**

> **A switch learns where hosts are by observing source MAC addresses, then uses the learned MAC-to-port mappings to make forwarding decisions.**

**Author:** Charles Muriuki
**BSc Information Technology**
**CYBERSECURITY MISSION 2028**
