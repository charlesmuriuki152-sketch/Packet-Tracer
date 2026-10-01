# Access Layer — VLAN Segmentation and Port Security

## Objective

To configure a Cisco switch to separate endpoint devices into different VLANs and apply basic port-security controls to access ports.

The lab demonstrates how an Access Layer switch can provide **network segmentation and basic endpoint access control**.

---

## Topology

```text
                    Switch0
                 Cisco 2960
              ┌─────┼─────┐
              │     │     │
             PC0   PC1   PC2   PC3
```

### Connections

| Device | Switch Port | VLAN    |
| ------ | ----------- | ------- |
| PC0    | Fa0/1       | VLAN 10 |
| PC1    | Fa0/2       | VLAN 10 |
| PC2    | Fa0/3       | VLAN 20 |
| PC3    | Fa0/4       | VLAN 20 |

All devices were connected using **Copper Straight-Through** cables.

---

## IP Addressing

| Device | VLAN | IP Address      | Subnet Mask     |
| ------ | ---: | --------------- | --------------- |
| PC0    |   10 | `192.168.10.10` | `255.255.255.0` |
| PC1    |   10 | `192.168.10.20` | `255.255.255.0` |
| PC2    |   20 | `192.168.20.10` | `255.255.255.0` |
| PC3    |   20 | `192.168.20.20` | `255.255.255.0` |

No default gateway was configured because the lab did not include a router or Layer 3 switch.

---

## VLAN Configuration

Two VLANs were created on the switch:

* **VLAN 10 — EMPLOYEES**
* **VLAN 20 — GUESTS**

### VLAN 10

```text
enable
configure terminal

vlan 10
name EMPLOYEES
exit
```

### VLAN 20

```text
vlan 20
name GUESTS
exit
```

---

## Access Port Configuration

PC0 and PC1 were assigned to VLAN 10:

```text
interface range fa0/1-2
switchport mode access
switchport access vlan 10
exit
```

PC2 and PC3 were assigned to VLAN 20:

```text
interface range fa0/3-4
switchport mode access
switchport access vlan 20
exit
```

The resulting logical segmentation was:

```text
VLAN 10 — EMPLOYEES
    │
    ├── PC0
    └── PC1

VLAN 20 — GUESTS
    │
    ├── PC2
    └── PC3
```

---

## VLAN Verification

The VLAN configuration was verified using:

```text
show vlan brief
```

The switch showed the access-port assignments:

```text
VLAN 10 → Fa0/1, Fa0/2
VLAN 20 → Fa0/3, Fa0/4
```

This confirmed that the switch ports had been assigned to the intended VLANs.

---

# Connectivity Testing

## Test 1 — VLAN 10

From PC0:

```text
ping 192.168.10.20
```

### Result

**Successful.**

PC0 and PC1 are members of VLAN 10.

---

## Test 2 — VLAN 20

From PC2:

```text
ping 192.168.20.20
```

### Result

**Successful.**

PC2 and PC3 are members of VLAN 20.

---

## Test 3 — Between VLANs

From PC0:

```text
ping 192.168.20.10
```

### Result

**No replies were received.**

PC0 belongs to VLAN 10 while PC2 belongs to VLAN 20.

The lab did not contain a router or Layer 3 switch to provide communication between the two VLANs.

This demonstrated the intended Layer 2 segmentation.

---

# Port Security

After verifying VLAN segmentation, basic port security was configured on the access ports.

The configuration used:

```text
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
```

The purpose was to restrict each access port to a maximum of one learned MAC address.

### Port Security Verification

The configuration was checked using:

```text
show port-security
```

and:

```text
show port-security address
```

Individual port security could also be inspected using:

```text
show port-security interface fa0/1
```

---

# Results

| Test            | Expected Result         | Observed Result |
| --------------- | ----------------------- | --------------- |
| PC0 → PC1       | Communication           | Successful      |
| PC2 → PC3       | Communication           | Successful      |
| PC0 → PC2       | No communication        | No replies      |
| VLAN assignment | Correct separation      | Confirmed       |
| Port security   | Enabled on access ports | Confirmed       |

---

# Security Significance

VLANs provide **network segmentation** at the Access Layer.

In this lab:

```text
VLAN 10 → EMPLOYEES
VLAN 20 → GUESTS
```

Devices belonging to different VLANs were separated at Layer 2.

Port security adds another security control by limiting the MAC addresses that can be learned and used on an access port.

These concepts are important foundations for understanding larger security architectures, including network segmentation, access control, and network monitoring.

---

# Troubleshooting

One important aspect of the lab was verifying the actual behavior rather than assuming that devices in different VLANs could communicate.

The connectivity tests demonstrated that:

```text
Same VLAN     → Communication successful
Different VLAN → No replies
```

This confirmed that the VLAN configuration was functioning as intended.

---

# Commands Used

```text
enable
configure terminal

vlan 10
name EMPLOYEES
exit

vlan 20
name GUESTS
exit

interface range fa0/1-2
switchport mode access
switchport access vlan 10
exit

interface range fa0/3-4
switchport mode access
switchport access vlan 20
exit

interface fa0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
exit

interface range fa0/2-4
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
exit

end

show vlan brief
show port-security
show port-security address
show port-security interface fa0/1
```

---

# Evidence

The lab evidence includes:
## Packet Tracer File

[Open Lab 6 Packet Tracer File](lab%206.pkt)

* VLAN configuration
* `show vlan brief` output
* Successful same-VLAN connectivity tests
* Failed cross-VLAN connectivity test
* Port-security verification

## Video Demonstration

[Watch the Access Layer VLAN and Port Security Lab](https://www.youtube.com/watch?v=tlJIdR5ZFN4)

---

# Conclusion

This lab demonstrated how a Cisco access switch can be used to provide **VLAN-based network segmentation** and **basic access-port security**.

Two separate VLANs were created and assigned to different switch ports. Devices within the same VLAN successfully communicated, while devices belonging to different VLANs did not receive replies because no Layer 3 routing was configured between the VLANs.

Port security was then applied to the access ports to provide an additional layer of control over connected devices.

The lab provided practical experience with **VLANs, access ports, Layer 2 segmentation, MAC-based port security, switch verification, and network troubleshooting**.

