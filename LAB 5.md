# Network Media — Lab 01: Ethernet Cable Types

## Objective

To practically compare **Copper Straight-Through** and **Copper Crossover** cables in Cisco Packet Tracer and observe their effect on network connectivity.

## Topology

```text
PC0 ─── Switch0 ─── Switch1 ─── PC1
```

### Connections

| Connection                      | Cable                   |
| ------------------------------- | ----------------------- |
| PC0 Fa0 → Switch0 Fa0/1         | Copper Straight-Through |
| Switch0 Fa0/24 → Switch1 Fa0/24 | Copper Crossover        |
| Switch1 Fa0/1 → PC1 Fa0         | Copper Straight-Through |

## IP Addressing

| Device | IP Address      | Subnet Mask     |
| ------ | --------------- | --------------- |
| PC0    | `192.168.10.10` | `255.255.255.0` |
| PC1    | `192.168.10.20` | `255.255.255.0` |

No default gateway was required.

---

## Experiment

First, the switches were connected using a **Copper Crossover** cable.

From PC0:

```text
ping 192.168.10.20
```

**Result:** Replies received successfully.

The crossover cable was then replaced with a **Copper Straight-Through** cable.

The ping test was repeated:

```text
ping 192.168.10.20
```

**Result:** Replies were still received successfully.

The crossover cable was then restored, and connectivity remained successful.

### Observation

Packet Tracer displays the cable types differently:

* **Copper Crossover:** Orange
* **Copper Straight-Through:** Green

The different cable colors represent the cable types and do not indicate a connection failure.

Both cable types successfully provided connectivity in this Packet Tracer experiment.

---

## Networking Concept

Traditionally:

```text
PC → Switch       = Straight-Through
Switch → Switch   = Crossover
```

However, devices supporting **Auto-MDI/MDIX** can automatically adapt to the cable type, allowing a straight-through cable to work where a crossover cable was traditionally required.

---

## Cybersecurity Connection

Understanding network media helps cybersecurity engineers troubleshoot physical connectivity and understand the infrastructure over which security monitoring and network traffic analysis take place.

---

## Video Evidence

### Click the Thumbnail Below to View My YouTube Video

[![Ethernet Cable Types — Straight-Through vs Crossover](https://img.youtube.com/vi/o6EhQyWjewc/maxresdefault.jpg)](https://www.youtube.com/watch?v=o6EhQyWjewc)
```

Replace `VIDEO_ID` with the ID of the uploaded video.

---

## Conclusion

This lab demonstrated the practical behavior of **Copper Straight-Through and Copper Crossover cables** in Packet Tracer. Both cables successfully supported communication between the two PCs, demonstrating the effect of **Auto-MDI/MDIX** in modern Ethernet interfaces.

**Lab Status: Completed ✅**
