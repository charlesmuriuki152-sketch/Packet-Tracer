# Lab 3: Configure a Wireless Router and Clients

## Overview
In this comprehensive hands-on lab, you will configure a complete home network setup in Cisco Packet Tracer. You'll connect network devices, configure a wireless router with security settings, and establish connectivity for both wired and wireless clients.

**Scenario:** Your friend Natsumi needs help setting up her home network to connect devices to the cable TV provider's internet service and configure a secure wireless network for her home.

---

## Objectives

By completing this lab, you will be able to:

### Part 1: Connect the Devices
- Connect coaxial cables from a cable splitter to appropriate devices
- Connect copper Ethernet cables between network devices
- Understand the role of each device in a home network

### Part 2: Configure the Wireless Router
- Access the wireless router's web-based GUI
- Configure basic router settings (DHCP, maximum users)
- Change default credentials and set a strong password
- Enable and configure a wireless LAN (WLAN)
- Implement WPA2 Personal security with a passphrase

### Part 3: Configure IP Addressing and Test Connectivity
- Configure DHCP on network clients
- Connect wireless devices to the wireless network
- Verify connectivity for all devices (wired and wireless)
- Test internet access from multiple hosts

---

## Background / Scenario

Your friend Natsumi recently moved to a new home and needs help connecting her devices to the internet. The cable TV provider delivers both internet and video services to her home through a coaxial cable. You need to:

1. **Connect the devices** using appropriate cable types
2. **Configure the wireless router** to manage her home network
3. **Set up security** to prevent unauthorized access
4. **Verify all devices** can connect and access the internet

---

## Network Topology

### Devices in this lab:
- **Cable Splitter** - Separates internet and video services
- **Cable Modem** - Connects to the internet service
- **Home Wireless Router** - Central device managing the network
- **Television** - Receives video service (coaxial connection)
- **Office PC** - Wired connection to router
- **Bedroom PC** - Wired connection to router
- **Laptop** - Wireless connection to router

### Connections:
```
Cable Outlet → Cable Splitter
                ├─→ Coaxial1 → Cable Modem → Router (Internet port)
                └─→ Coaxial2 → Television

Router Ports:
├─→ GigabitEthernet 1 → Office PC
├─→ GigabitEthernet 2 → Bedroom PC
└─→ Wireless (2.4 GHz) → Laptop
```

---

## Step-by-Step Instructions

### **PART 1: Connect the Devices**

#### Step 1: Connect Coaxial Cables

1. Open Cisco Packet Tracer and load the lab file
2. In **Network Components**, click **Connections** (lightning bolt icon)
3. Select **Coaxial cable** (blue zigzag icon)
4. Connect **Cable Splitter (Coaxial1)** → **Cable Modem (Port 0)**
5. Connect **Cable Splitter (Coaxial2)** → **Television (Port 0)**
6. Click the TV and set **Status to ON**
   - ✅ If configured correctly, you should see a TV program image

#### Step 2: Connect Network Cables (Ethernet)

1. Click **Connections** → **Copper Straight-Through cable** (solid black line)
2. Connect **Cable Modem (Port 1)** → **Home Wireless Router (Internet port)**
3. Connect **Office PC (FastEthernet0)** → **Home Wireless Router (GigabitEthernet 1)**
4. Connect **Bedroom PC (FastEthernet0)** → **Home Wireless Router (GigabitEthernet 2)**

✅ **Wired network is now connected to the internet!**

---

### **PART 2: Configure the Wireless Router**

#### Step 1: Access the Router's Web GUI

1. Click **Office PC** → **Desktop tab** → **IP Configuration**
2. Select **DHCP** to automatically configure the PC
3. Wait for the IPv4 address to update (should start with `192`)
4. Note the **Default Gateway** address (this is the router's IP)
5. Close **IP Configuration** and open **Web Browser**
6. Enter the router's IP address (default gateway) in the URL box
7. **Login Credentials:**
   - Username: `admin`
   - Password: `admin`

✅ **You should now see the router's GUI interface**

#### Step 2: Configure Basic Settings

1. You're on the **Setup tab** - look for **Network Setup**
2. Find the **Maximum Number of Users** field
3. Change the value to: `10`
   - (Natsumi only expects ~10 devices max)
4. **Scroll down and click Save Settings**

5. Click the **Administration tab**
6. Change the password:
   - New Password: `MyPassword1!`
   - Confirm Password: `MyPassword1!`
7. **Scroll down and click Save Settings**
8. When prompted, login with:
   - Username: `admin`
   - Password: `MyPassword1!`

✅ **Router credentials are now secured**

#### Step 3: Configure the Wireless LAN

1. Click the **Wireless tab**
2. For the **2.4 GHz network**, click **Enable** to activate the radio
3. Change the **Network Name (SSID)** from "Default" to: `MyHome`
4. **Scroll down and click Save Settings**

5. Scroll back up and click **Wireless Security** (under Wireless tab)
6. For the **2.4 GHz network**, click the dropdown and select: `WPA2 Personal`
7. Enter the **Passphrase**: `MyPassPhrase1!`
   - ⚠️ **Note: Capitalization is important!**
8. **Scroll down and click Save Settings**
9. **Close the Web Browser**

✅ **Wireless network is now configured and secured!**

---

### **PART 3: Configure IP Addressing and Test Connectivity**

#### Step 1: Connect the Laptop to Wireless Network

1. Click **Laptop** → **Desktop tab** → **PC Wireless**
2. Click the **Connect tab**
3. Wait for the wireless network list to appear
4. Select **MyHome** from the list
5. Click **Connect**
6. Enter the **Pre-shared Key**: `MyPassPhrase1!`
7. Click **Connect**
8. Click the **Link Information tab**
   - ✅ You should see: "You have successfully connected to the access point"
9. Click **More Information** to view connection details
10. Verify the IP address starts with `192`
11. Close **PC Wireless** and open **Web Browser**
12. Navigate to: `skillsforall.srv`
    - ✅ If the page loads, wireless internet connectivity is working!

#### Step 2: Verify Office PC Internet Access

1. Click **Office PC** → **Desktop tab** → **Web Browser**
2. Enter: `skillsforall.srv`
3. Click **Go**
   - ✅ Webpage should load, confirming wired internet connectivity

#### Step 3: Configure Bedroom PC

1. Click **Bedroom PC** → **Desktop tab** → **IP Configuration**
2. Select **DHCP**
3. Verify the IP address starts with `192`
4. Close **IP Configuration** and open **Web Browser**
5. Enter: `skillsforall.srv`
6. Click **Go**
   - ✅ If the page loads, all devices have internet connectivity!

---

## Key Concepts Learned

| Concept | Description |
|---------|-------------|
| **DHCP** | Automatically assigns IP addresses to network devices |
| **Wireless SSID** | Network name broadcast for wireless devices to discover |
| **WPA2 Personal** | Strong wireless encryption using a pre-shared key (passphrase) |
| **Default Gateway** | Device that provides access to external networks (the router) |
| **Coaxial Cable** | Used for cable TV and internet delivery from provider |
| **Ethernet Cable** | Used for wired network connections between devices |
| **Network Segmentation** | Limiting DHCP to 10 users controls network size and security |

---

## Security Best Practices Applied

✅ **Changed default credentials** - Router password changed from "admin/admin"  
✅ **Enabled WPA2 encryption** - Protects wireless traffic from eavesdropping  
✅ **Strong passphrase** - `MyPassPhrase1!` uses mixed case and special characters  
✅ **Limited DHCP scope** - Max 10 users prevents resource exhaustion  
✅ **SSID broadcast** - Enabled for ease of use (could be hidden for additional security)

---

## Troubleshooting Guide

### Issue: Laptop won't connect to wireless network
**Solution:** 
- Verify SSID name is exactly `MyHome` (case-sensitive)
- Confirm passphrase is `MyPassPhrase1!` (with capital M and P)
- Ensure WPA2 Personal is selected as security type
- Click "Fast Forward Time" to speed up simulation

### Issue: PC doesn't get 192.x.x.x IP address
**Solution:**
- Click "Fast Forward Time" several times to allow DHCP to complete
- Toggle between DHCP and Static in IP Configuration
- Verify the router is powered on and connected

### Issue: Web browser won't load skillsforall.srv
**Solution:**
- Verify the device has a 192.x.x.x IP address
- Click "Fast Forward Time" multiple times for pages to load
- Confirm all cables are connected properly
- Check router GUI to confirm settings were saved

---

## 📺 YouTube Video Walkthrough

**Watch the complete lesson here:**

[![Cisco Packet Tracer Wireless Router Configuration](https://img.youtube.com/vi/6AhZafYA52E/0.jpg)](https://www.youtube.com/watch?v=6AhZafYA52E&t=60s)

**[Cisco Packet Tracer Wireless Router Configuration - Full Tutorial](https://www.youtube.com/watch?v=6AhZafYA52E&t=60s)**

This video provides a visual walkthrough of the entire lab, showing how to:
- Connect all devices properly
- Configure the router GUI
- Set up wireless security
- Test connectivity from all devices

---

## What I Learned

Through completing this lab, I reinforced:

✅ **Network device roles** - Understanding how modems, routers, and devices interact  
✅ **Wireless security** - Importance of strong encryption and passphrases  
✅ **DHCP configuration** - How automatic IP addressing simplifies network management  
✅ **Hands-on troubleshooting** - Systematically testing each device and connection  
✅ **Home network design** - Creating a secure, functional network for multiple devices  
✅ **Security best practices** - Changing defaults and enabling encryption  
✅ **Practical networking** - Real-world scenario of setting up a home network  

---

## Real-World Applications

This lab simulates real scenarios you'd encounter:
- Setting up a new home or office network
- Configuring guest Wi-Fi for visitors
- Securing personal wireless networks
- Troubleshooting connectivity issues
- Balancing security and usability

---

## Future Enhancements

This lab could be expanded to include:
- Guest network configuration (separate SSID)
- MAC address filtering for additional security
- VLAN setup for network segmentation
- Port forwarding for remote services
- Dynamic DNS for remote access
- Wireless monitoring and signal strength analysis
- WPA3 configuration (newer security standard)

---

## Files Included

- `Wireless-Router-Config-Lab.pkt` - Complete lab file ready to open in Cisco Packet Tracer
- `README.md` - This comprehensive guide (you are here)

---

## Prerequisites

- **Cisco Packet Tracer** (version 7.0 or higher, preferably 8.0+)
- Basic understanding of networking concepts
- Familiarity with the Packet Tracer interface
- Understanding of IP addressing (192.168.x.x networks)

---

## Completion Checklist

- [ ] All coaxial cables connected correctly
- [ ] All Ethernet cables connected properly
- [ ] TV displays program image
- [ ] Accessed router GUI successfully
- [ ] Changed router password to `MyPassword1!`
- [ ] Set maximum users to 10
- [ ] Configured SSID to `MyHome`
- [ ] Enabled WPA2 Personal security
- [ ] Set passphrase to `MyPassPhrase1!`
- [ ] Laptop connected to wireless network
- [ ] All devices (Office PC, Bedroom PC, Laptop) access skillsforall.srv successfully
- [ ] All devices have 192.x.x.x IP addresses

✅ **If all items are checked, the lab is complete!**

---

## Notes for Recruiters/Reviewers

This lab demonstrates:
- **Hands-on networking experience** with industry-standard tools
- **Security awareness** through WPA2 implementation and password management
- **Problem-solving skills** in network configuration and troubleshooting
- **Practical knowledge** of home/small office networks
- **Attention to detail** in following complex multi-step procedures
- **Foundation for advanced certifications** (CCNA, Security+, CEH)

---

## Lab Statistics

- **Estimated Completion Time:** 45-60 minutes
- **Difficulty Level:** Beginner to Intermediate
- **Devices Configured:** 7 (1 Router, 3 PCs, 1 Modem, 1 TV, 1 Splitter)
- **Security Features Implemented:** 3 (WPA2, Strong Password, DHCP Limits)
- **Concepts Covered:** 12+ networking fundamentals

---

*Lab completed as part of ongoing cybersecurity and networking education.*  
*Original lab from Cisco Skills for All - Packet Tracer Activities*  
*Documentation updated: 2026-09-26*
