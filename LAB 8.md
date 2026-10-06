# Lab: Router as a Broadcast Domain Boundary

## Objective

To demonstrate how a router separates two different IPv4 networks into separate broadcast domains and prevents an IPv4 broadcast from being forwarded from one network to another.

---

## Network Topology

```text
                    ROUTER
             ┌─────────────────┐
             │                 │
PC0 ── Switch0 ── G0/0     G0/1 ── Switch1 ── PC1
             │                 │
             └─────────────────┘

     192.168.10.0/24       192.168.20.0/24
```

---

## Devices Used

* 2 × PCs
* 2 × Cisco switches
* 1 × Cisco router
* Copper Ethernet cables

---

## IP Addressing

| Device | Interface     | IP Address      | Subnet Mask     | Default Gateway |
| ------ | ------------- | --------------- | --------------- | --------------- |
| PC0    | FastEthernet0 | `192.168.10.10` | `255.255.255.0` | `192.168.10.1`  |
| Router | G0/0          | `192.168.10.1`  | `255.255.255.0` | —               |
| Router | G0/1          | `192.168.20.1`  | `255.255.255.0` | —               |
| PC1    | FastEthernet0 | `192.168.20.10` | `255.255.255.0` | `192.168.20.1`  |

### Networks

**Network 1:**

`192.168.10.0/24`

Broadcast address:

`192.168.10.255`

**Network 2:**

`192.168.20.0/24`

Broadcast address:

`192.168.20.255`

---

# Part 1 — Configure the Router

Open the router's **CLI**.

Enter privileged EXEC mode:

```text
enable
```

Enter global configuration mode:

```text
configure terminal
```

### Configure G0/0

```text
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
```

### Configure G0/1

```text
interface gigabitEthernet 0/1
ip address 192.168.20.1 255.255.255.0
no shutdown
```

Exit configuration mode:

```text
end
```

Verify the interfaces:

```text
show ip interface brief
```

The router should have:

```text
G0/0    192.168.10.1
G0/1    192.168.20.1
```

with both interfaces operational.

---

# Part 2 — Configure the PCs

## PC0

Configure:

```text
IP Address:       192.168.10.10
Subnet Mask:      255.255.255.0
Default Gateway:  192.168.10.1
```

## PC1

Configure:

```text
IP Address:       192.168.20.10
Subnet Mask:      255.255.255.0
Default Gateway:  192.168.20.1
```

---

# Part 3 — Test Normal Unicast Communication

A normal ping between PC0 and PC1 is a **unicast** communication.

From PC0:

```text
ping 192.168.20.10
```

The packet has a specific destination:

```text
192.168.20.10
```

Therefore, the router can route the packet from:

```text
192.168.10.0/24
```

to:

```text
192.168.20.0/24
```

The path is:

```text
PC0
 ↓
Switch0
 ↓
Router G0/0
 ↓
Router G0/1
 ↓
Switch1
 ↓
PC1
```

This demonstrates that the router **can forward Layer-3 unicast traffic between the two networks**.

---

# Part 4 — Generate a Broadcast

The broadcast address of the first network is:

```text
192.168.10.255
```

From PC0, the broadcast can be targeted at:

```text
ping 192.168.10.255
```

The important point is that `192.168.10.255` is the broadcast address for:

```text
192.168.10.0/24
```

The broadcast belongs to the first network.

---

# Part 5 — Observe the Router Boundary

Use **Simulation Mode** in Packet Tracer.

The broadcast originates on the:

```text
192.168.10.0/24
```

network.

It can reach the router through:

```text
G0/0
```

However, the router does **not** simply forward that same Layer-3 broadcast out of:

```text
G0/1
```

into:

```text
192.168.20.0/24
```

Therefore, the broadcast does not become a broadcast in the second network.

The two networks remain separate broadcast domains.

---

# What the Lab Demonstrates

The router has two interfaces:

```text
G0/0 → 192.168.10.0/24
G0/1 → 192.168.20.0/24
```

Each interface belongs to a different IP network.

Therefore:

```text
Broadcast Domain 1
192.168.10.0/24
        │
        │
      ROUTER
        │
        │
Broadcast Domain 2
192.168.20.0/24
```

A router does not forward normal IPv4 broadcasts between these interfaces by default.

---

# Unicast vs Broadcast

## Unicast

A unicast has one specific destination.

Example:

```text
PC0 → PC1
192.168.10.10 → 192.168.20.10
```

The router can route this traffic.

```text
PC0
 ↓
Router
 ↓
PC1
```

## Broadcast

A broadcast is intended for all devices within the relevant broadcast domain.

Example:

```text
192.168.10.255
```

The router does not forward this broadcast into the other network by default.

```text
192.168.10.0/24
       ↓
     Router
       X
192.168.20.0/24
```

---

# Key Observation

The important difference observed in this lab is:

**Unicast traffic can be routed between the two networks, while an IPv4 broadcast is not forwarded across the router by default.**

This demonstrates why the router acts as a **boundary between broadcast domains**.

---

# Why the Default Gateway Was Required

PC0 and PC1 belong to different IP networks.

PC0 belongs to:

```text
192.168.10.0/24
```

PC1 belongs to:

```text
192.168.20.0/24
```

When PC0 needs to communicate with a destination outside its own subnet, it sends the traffic to its default gateway:

```text
192.168.10.1
```

The router then determines where to forward the Layer-3 packet.

Similarly, PC1 uses:

```text
192.168.20.1
```

as its default gateway.

The default gateway therefore allows **unicast routing between the networks**. It does not cause the router to forward broadcasts.

---

# Verification Commands

## Router

```text
show ip interface brief
```

Shows the IP addresses and operational status of the router interfaces.

## PC0

```text
ping 192.168.10.1
```

Tests connectivity to the router's first interface.

```text
ping 192.168.20.10
```

Tests routed connectivity to PC1.

## PC1

```text
ping 192.168.20.1
```

Tests connectivity to the router's second interface.

```text
ping 192.168.10.10
```

Tests routed connectivity to PC0.

---

# Final Conclusion

This lab demonstrated that a router separates different IPv4 networks into different broadcast domains.

The router successfully provides Layer-3 communication between:

```text
192.168.10.0/24
```

and

```text
192.168.20.0/24
```

for unicast traffic.

However, an IPv4 broadcast generated within one network is not forwarded into the other network by default.

## To view my lab on my youtube channel click the following thumnail

[![Router Domain Separation Lab](https://img.youtube.com/vi/lqrrxJBPx7U/maxresdefault.jpg)](https://www.youtube.com/watch?v=lqrrxJBPx7U)


This is one of the fundamental differences between the roles of **switches and routers** in a network.
