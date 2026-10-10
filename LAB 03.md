# Lab 01 — Ethernet Communication and Packet Observation

> **Cisco Packet Tracer Practical Lab | Communications Principles**

---

## 📌 Lab Overview

This practical lab was created to apply concepts from the **Communications Principles** section of Cisco Networking Basics using Cisco Packet Tracer.

The lab uses two PCs connected through a Layer 2 switch. Packet Tracer's **Simulation Mode** was used to observe how communication moves through the network.

The main focus of this lab was to move beyond theory and **observe actual packet movement between network devices**.

---

# 🎯 Objectives

The objectives of this practical were to:

* Build a basic Ethernet network.
* Connect end devices through a switch.
* Configure IPv4 addresses.
* Test communication between two PCs.
* Observe packet movement using Simulation Mode.
* Identify the path taken by traffic through the switch.
* Observe different packet events during communication.
* Relate the practical behavior to Ethernet networking concepts.

---

# 🧰 Tools and Devices

### Software

* Cisco Packet Tracer
* Cisco Networking Academy — Networking Basics

### Devices

* 2 × PCs
* 1 × Cisco 2960 switch
* Copper Straight-Through Ethernet cables

---

# 🌐 Network Topology

```text
PC0
 │
 │ FastEthernet0
 │
 │
Switch0
 │
 │
 │ FastEthernet0
 │
PC1
```

### Connections

| Device | Interface     | Connected Device | Interface       |
| ------ | ------------- | ---------------- | --------------- |
| PC0    | FastEthernet0 | Switch0          | FastEthernet0/1 |
| PC1    | FastEthernet0 | Switch0          | FastEthernet0/2 |

---

# 🖥️ IP Addressing

| Device | IPv4 Address   | Subnet Mask     |
| ------ | -------------- | --------------- |
| PC0    | `192.168.1.10` | `255.255.255.0` |
| PC1    | `192.168.1.20` | `255.255.255.0` |

Both PCs are configured within the same IPv4 network:

```text
192.168.1.0/24
```

No default gateway was required for communication between the two PCs because they are on the same local network.

---

# 🔧 Configuration

## PC0

I configured PC0 with:

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
```

## PC1

I configured PC1 with:

```text
IP Address: 192.168.1.20
Subnet Mask: 255.255.255.0
```

---

# 🧪 Practical Procedure

### Step 1 — Build the topology

I placed two PCs and one Cisco 2960 switch into the Packet Tracer workspace.

### Step 2 — Connect the devices

I connected:

```text
PC0 FastEthernet0 → Switch0 FastEthernet0/1
PC1 FastEthernet0 → Switch0 FastEthernet0/2
```

using Copper Straight-Through cables.

### Step 3 — Configure the PCs

I assigned the IPv4 addresses shown above.

### Step 4 — Enter Simulation Mode

I switched Packet Tracer from **Realtime Mode** to **Simulation Mode** so that I could observe the communication step by step.

### Step 5 — Create a Simple PDU

I used the **Add Simple PDU** tool to initiate communication from:

```text
PC0 → PC1
```

I then observed the resulting packet movement in the simulation.

---

# 🔬 Practical Observation

During the Packet Tracer simulation, I observed the following sequence:

### First exchange

A **green envelope** traveled:

```text
PC0 → Switch0 → PC1
```

### Return exchange

A **green envelope** then traveled:

```text
PC1 → Switch0 → PC0
```

The communication completed successfully.

### Additional packet event

After this exchange, a **pink envelope** appeared at **Switch0** and was forwarded toward both connected PCs.

The important point from the practical observation is that I could see **different packet events occurring during the communication**, rather than simply seeing the PCs as connected.

---

# 🧠 What I Discovered

## 1. The switch is involved in communication between the PCs

The simulation showed that traffic between PC0 and PC1 passed through Switch0:

```text
PC0
 ↓
Switch0
 ↓
PC1
```

The return communication also passed through the switch:

```text
PC1
 ↓
Switch0
 ↓
PC0
```

This gave me a practical understanding of the role of a switch in connecting devices within a local Ethernet network.

---

## 2. Network communication can involve multiple packet events

The simulation showed more than one packet event.

I observed:

```text
PC0 → Switch0 → PC1
```

followed by:

```text
PC1 → Switch0 → PC0
```

and then another packet event involving the switch and both connected PCs.

This helped me understand that a simple communication test can involve multiple network operations taking place between devices.

---

## 3. Packet Tracer allows network communication to be observed

In a normal network, packet transmission happens extremely quickly and is difficult to observe directly.

Simulation Mode allowed me to slow down the process and observe individual events as they occurred.

This makes Packet Tracer useful for connecting networking theory with practical behavior.

---

# 📡 Broadcast and Flooding — What This Lab Taught Me

The pink envelope was observed leaving the switch and being sent toward both connected PCs.

However, **the visual movement alone is not enough to establish exactly why the switch forwarded that packet to multiple devices**.

Therefore, this lab should not claim that the observation itself proves:

* the packet was an ARP request,
* the packet was definitely a broadcast,
* the switch was performing unknown-unicast flooding,
* or a specific MAC-learning event occurred.

Those conclusions require inspection of the packet's details and, where appropriate, the switch's MAC address table.

What the practical **does establish from the observation** is that the switch can be involved in forwarding a packet toward multiple connected devices during network communication.

---

# 🔑 MAC Addresses and Switching

A major concept associated with this lab is the role of **MAC addresses in Ethernet switching**.

A Layer 2 switch uses MAC-address information when making forwarding decisions.

A simplified representation is:

```text
Ethernet Frame
      ↓
Switch receives frame
      ↓
Examines MAC information
      ↓
Makes forwarding decision
      ↓
Forwards the frame
```

However, this particular observation does **not by itself demonstrate the complete MAC-learning process**.

A dedicated MAC-learning practical can be used later to inspect the switch's MAC address table directly and document that process with evidence.

---

# 📢 Broadcast vs Flooding

These terms should not be treated as identical.

### Broadcast

A broadcast Ethernet frame uses the destination MAC address:

```text
FFFF.FFFF.FFFF
```

It is intended for all appropriate devices within the broadcast domain.

### Unknown Unicast Flooding

A switch may also flood a frame when it does not yet know which interface contains the destination MAC address.

Therefore:

```text
Multiple devices receiving traffic
            ≠
Automatically a broadcast
```

The packet's PDU information must be inspected to determine the exact reason.

This distinction is important for accurate networking documentation.

---

# 🛠️ Challenges Encountered

## Challenge 1 — Locating the Simple PDU Tool

Initially, finding the **Add Simple PDU** tool in Packet Tracer was challenging.

I learned how to locate and use the envelope tool to generate a communication test between devices.

---

## Challenge 2 — Understanding the Packet Animation

Initially, the packet animation was difficult to interpret because multiple events appeared during a simple communication test.

Using Simulation Mode allowed me to slow down the process and observe the sequence more carefully.

---

## Challenge 3 — Understanding Traffic Sent Toward Multiple Devices

I observed the pink envelope being forwarded toward both connected PCs.

This raised the question of why the switch was forwarding the packet to multiple devices.

This led to an important networking lesson: **the animation should not be used alone to identify a packet's exact protocol or forwarding reason.**

PDU details provide the necessary evidence.

---

# 🔧 Troubleshooting

The following configuration details were checked during the practical:

### PC0

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
```

### PC1

```text
IP Address: 192.168.1.20
Subnet Mask: 255.255.255.0
```

### Switch connections

```text
PC0 Fa0 → Switch0 Fa0/1
PC1 Fa0 → Switch0 Fa0/2
```

### Network

```text
192.168.1.0/24
```

The successful completion of the communication demonstrated that the basic topology and addressing were functioning.

---

# 🔐 Cybersecurity Connection

This practical provides a foundation for cybersecurity because many security investigations require understanding **normal network communication first**.

The concepts introduced here connect to future security topics such as:

* ARP security
* Packet analysis
* Network monitoring
* MAC address security
* Network reconnaissance
* Network segmentation
* Traffic analysis
* Intrusion detection

Understanding normal Ethernet communication makes it easier to recognize unusual network behavior later.

---

## 📸 Evidence

### 🎥 Practical Demonstration

[![Lab 01](https://img.youtube.com/vi/z6X-zTEoYvI/maxresdefault.jpg)](https://www.youtube.com/watch?v=z6X-zTEoYvI)
**▶️ Click the thumbnail to watch the practical demonstration.**

The video demonstrates the Packet Tracer topology, communication test, Simulation Mode, and observed packet movement.

**MAC Address Table:** Verified directly from the Switch0 CLI using:

```text
enable
show mac address-table
```
---

# 📚 Key Lessons

From this practical, I learned that:

1. **A switch is an intermediary device through which the PCs communicate.**

2. **Traffic can travel in both directions between communicating devices.**

3. **A single communication test can involve multiple packet events.**

4. **Packet Tracer Simulation Mode makes network communication visible and easier to analyze.**

5. **Seeing a packet forwarded toward multiple devices does not automatically prove that it is a broadcast.**

6. **PDU information is important when determining exactly what is happening to a packet.**

7. **Accurate networking analysis requires distinguishing between what is observed and what is concluded from the evidence.**

---

# 🎯 Skills Demonstrated

### Networking

* Ethernet communication
* IPv4 addressing
* Subnetting fundamentals
* Layer 2 switching concepts
* Packet-flow observation

### Cisco Packet Tracer

* Topology creation
* Device connections
* IPv4 configuration
* Simulation Mode
* Simple PDU testing
* Packet observation

### Cybersecurity Foundation

* Network traffic observation
* Evidence-based analysis
* Ethernet security concepts
* Packet-analysis fundamentals
* Network troubleshooting

### Documentation

* Practical lab documentation
* Recording observations
* Recording challenges
* Connecting theory with practical results
* Building technical evidence for a GitHub portfolio

---

# 📝 Conclusion

This practical demonstrated how two PCs communicate through a Layer 2 switch and allowed me to observe the communication process using Cisco Packet Tracer Simulation Mode.

The most important outcome was not simply that the two PCs successfully communicated. The simulation allowed me to **see the traffic moving through the switch and observe additional packet activity occurring during the communication**.

The lab therefore provided a practical foundation for further investigation into:

* MAC address learning
* ARP
* Broadcast communication
* Unicast communication
* Unknown-unicast flooding
* Ethernet frame forwarding

These concepts will be investigated more deeply in subsequent practical labs rather than being assumed from this single observation.

---

# 🚀 Next Practical

**Next Lab: Ethernet Unicast Communication**

The next lab will investigate how a switch handles traffic when the destination is known and will provide a clearer comparison between **unicast forwarding and traffic that is forwarded to multiple ports**.

---

## 👤 Author

**Charles Muriuki**

BSc Information Technology
**CYBERSECURITY MISSION 2028**

> **Learn → Build → Observe → Analyze → Document**
