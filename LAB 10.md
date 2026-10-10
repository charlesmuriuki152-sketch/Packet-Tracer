# Packet Tracer – Examine NAT on a Wireless Router

## Objectives

* Examine NAT configuration on a wireless router.
* Connect four PCs using DHCP.
* Observe NAT translation between private and public networks.

## Part 1: Examine the External Network

1. Add a PC and connect it to the wireless router using a straight-through cable.
2. Open **Desktop → IP Configuration** and select **DHCP**.
3. Note the default gateway.
4. Open the web browser and enter the gateway IP address.
5. Log in using `admin` for both username and password.
6. Navigate to **Status → Router** and examine the Internet connection IP address assigned by the ISP.

## Part 2: Examine the Internal Network

1. Navigate to **Status → Local Network**.
2. Examine the internal IP address and DHCP server settings.
3. Note the DHCP address range assigned to connected devices.

## Part 3: Connect Four PCs

1. Add three more PCs and connect them to the wireless router using straight-through cables.
2. On each PC, select **Desktop → IP Configuration → DHCP**.
3. Open Command Prompt and verify the configuration:

```text
ipconfig /all
```

4. Confirm that all PCs receive private IP addresses and the correct default gateway.

## Part 4: Observe NAT Translation

1. Switch to **Simulation** mode.
2. Open **Edit Filters** and select TCP and HTTP under the Misc tab.
3. Create a Complex PDU using a PC as the source and `ciscolearn.nat.com` as the destination.
4. Set the application to HTTP, source port to `1000`, and interval to `120` seconds. Select Periodic.
5. Click **Create PDU**, then **Play** to observe traffic flow.

## Part 5: Examine Packet Headers

1. Select an event in the Simulation Panel and open its packet envelope.
2. Examine the **Inbound PDU Details** and record the source and destination IP addresses.
3. Examine the **Outbound PDU Details** and compare the addresses.
4. Observe how NAT changes the source IP address as traffic passes through the wireless router.
5. Click **Check Results** when finished.

## Conclusion

This lab demonstrated how a wireless router uses DHCP to assign private IP addresses to PCs and NAT to translate private source addresses into the router's Internet-facing address. Packet Tracer's Simulation mode was used to examine packet headers and observe NAT in action.
## ## Cisco NAT Lab Tutorial

[![Watch Cisco NAT Lab Tutorial](https://img.youtube.com/vi/DsSRdRdOYmU/0.jpg)](https://www.youtube.com/watch?v=DsSRdRdOYmU)

**Click the thumbnail above to watch the video on YouTube.**
