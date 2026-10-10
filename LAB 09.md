# 🌐 DHCP (Dynamic Host Configuration Protocol)

## 📖 Overview

DHCP automatically assigns IP addresses and other network configuration settings to devices, allowing them to communicate over a network without manual configuration.

## ⚙️ How DHCP Works (DORA)

1. **Discover** – The client broadcasts a request to find a DHCP server.
2. **Offer** – The DHCP server offers an available IP address.
3. **Request** – The client requests the offered IP address.
4. **Acknowledgment (ACK)** – The server confirms the IP address assignment.

## 🖥️ DHCP Configuration on a Cisco Router

```cisco
enable
configure terminal
ip dhcp pool LAN_POOL
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
exit
```

## 🔍 Verification Commands

```cisco
show ip dhcp binding
show ip dhcp pool
show running-config
```

## 🎯 Benefits of DHCP

* Automatically assigns IP addresses.
* Reduces manual configuration errors.
* Prevents IP address conflicts when leases are managed correctly.
* Simplifies network administration.

## 🧪 Lab Objectives

* Understand the DHCP DORA process.
* Configure a Cisco router as a DHCP server.
* Verify IP address assignments.
* Test network connectivity in Cisco Packet Tracer.

## 🛠️ Tools

* Cisco Packet Tracer
* Cisco Router
* Switch and end devices

## 👨‍💻 Author

**Charles Muriuki**

Happy Networking! 🚀

#DHCP #Cisco #CCNA #Networking #PacketTracer

## I did this activity assigned by cisco to check my understanding:

### 📁 Cisco Packet Tracer Labs

* [📡 Configure DHCP on a Wireless Router (1).pka](https://github.com/charlesmuriuki152-sketch/Packet-Tracer/blob/main/Configure%20DHCP%20on%20a%20Wireless%20Router%20%281%29.pka)

 

 ### 🎥 Watch the Tutorial on YouTube

[![Watch on YouTube](https://img.youtube.com/vi/EoJ_EK_HpD0/maxresdefault.jpg)](https://www.youtube.com/watch?v=EoJ_EK_HpD0)

**▶️ Click the thumbnail above to watch the full tutorial on YouTube!**
