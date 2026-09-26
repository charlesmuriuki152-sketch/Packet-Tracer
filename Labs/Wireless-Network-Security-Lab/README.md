# Wireless Network Security Lab

This lab introduces a secure wireless network setup using Cisco Packet Tracer. It focuses on configuring a wireless access point, protecting the network with Wi-Fi security, and verifying connectivity for wireless clients.

---

## Lab Overview

In this exercise, you will build a small wireless LAN with:
- One wireless router or access point
- One switch (optional for wired connectivity)
- One server or DHCP source (optional)
- One wireless client such as a laptop or tablet

The goal is to configure a secure SSID, set a strong wireless password, and confirm that devices can connect successfully.

---

## Objectives

- Configure a wireless network in Cisco Packet Tracer
- Create a secure SSID
- Enable WPA2 security with a strong passphrase
- Assign DHCP or static addressing as needed
- Test connectivity from a wireless client

---

## Network Topology

A basic layout can include:
- Router / Wireless Router
- Access Point (or integrated wireless router)
- Switch
- Laptop / PC client
- Optional server for DHCP or internet access

---

## Step-by-Step Configuration

### 1. Add Network Devices
Open Cisco Packet Tracer and place the following devices on the workspace:
- Wireless Router / Access Point
- One laptop or wireless client
- One switch if needed
- One router or server if you want internet or DHCP support

### 2. Connect Devices
- Connect the wireless router to the switch or router using Ethernet.
- Connect the laptop to the wireless network using the wireless interface.
- If used, connect the switch to a router for internet access.

### 3. Configure the Wireless Router
Access the wireless router settings and configure:
- SSID: `SecureLabWiFi`
- Security Mode: `WPA2-PSK`
- Passphrase: `SecurePass@2026`
- Channel: default or auto
- DHCP: enabled for wireless clients

### 4. Configure the Client
On the laptop or wireless device:
- Open the wireless settings
- Select the SSID `SecureLabWiFi`
- Enter the wireless key
- Confirm the client obtains an IP address from DHCP

### 5. Validate Connectivity
From the client:
- Ping the default gateway
- Ping another device on the network
- Confirm successful communication and internet access if configured

---

## Security Best Practices

- Use a strong Wi-Fi password
- Prefer WPA2 or WPA3 over WEP
- Disable SSID broadcast only if your environment requires it
- Keep firmware updated where applicable
- Segment guest and internal networks where possible

---

## Troubleshooting Tips

If the wireless client cannot connect:
- Confirm the SSID matches exactly
- Check the password and encryption type
- Ensure DHCP is enabled
- Verify the wireless device is within range
- Check whether the router/AP interface is active

---

## YouTube Video Walkthrough

Watch a practical wireless configuration tutorial here:
[YouTube: Cisco Packet Tracer Wireless Network Configuration](https://www.youtube.com/results?search_query=Cisco+Packet+Tracer+Wireless+Network+Configuration)

---

## What I Learned

This lab reinforced several important concepts:
- Wireless networks require both hardware and security configuration
- Secure SSIDs and strong passwords are critical for protection
- DHCP and addressing are essential for client connectivity
- Troubleshooting is a core skill in packet-based wireless labs

---

## Notes

This guide is designed as a hands-on lab companion and can be expanded with advanced topics such as:
- VLAN-based wireless segmentation
- Access Control Lists (ACLs)
- Guest Wi-Fi isolation
- WPA3 improvements
- Wireless monitoring and troubleshooting

---

*Lab created as part of ongoing networking and cybersecurity practice.*
