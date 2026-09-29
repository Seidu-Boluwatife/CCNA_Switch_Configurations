# CCNA_Switch_Configurations
This Lab Shows the Catalyst 2960  Switch Configuration and Connection Verification
# Lab: View Network Device MAC Addresses

Configured a Cisco Catalyst 2960 (S1) and a PC (PC-A) on a simple LAN, verified connectivity, then used `ipconfig /all` and switch show commands to analyze Ethernet MAC addresses.

## Objectives

- **Part 1:** Configure devices and verify connectivity
- **Part 2:** Display, describe, and analyze Ethernet MAC addresses

## Topology and Addressing

| Device | Interface | IP Address  | Subnet Mask   |
|--------|-----------|-------------|---------------|
| S1     | VLAN 1    | 192.168.1.2 | 255.255.255.0 |
| PC-A   | NIC       | 192.168.1.3 | 255.255.255.0 |

PC-A connects to S1 on **F0/6**. The switch was configured via the console port using Tera Term.

## Part 1: Configure Devices and Verify Connectivity

**1. Cabled the network** as per the topology (console cable to S1, Ethernet cable from PC-A to F0/6).

**2. Configured PC-A** with IP `192.168.1.3` and mask `255.255.255.0`.

**3. Configured S1:**

```
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.2 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# end
S1# copy running-config startup-config
```

**4. Verified connectivity** by pinging S1 from PC-A:

```
C:\> ping 192.168.1.2
```
## Part 2: Display, Describe, and Analyze Ethernet MAC Addresses

A MAC address is 48 bits, shown as six hex pairs. The first 3 bytes are the **OUI** (vendor, assigned by the IEEE) and the last 3 bytes are the **NIC serial number** (assigned by the manufacturer). The same address can be written three ways:

```
00-05-9A-3C-78-00    00:05:9A:3C:78:00    0005.9A3C.7800
```

### Step 1: PC-A NIC MAC address

Command used: `ipconfig /all` (MAC shown as "Physical Address").

| Item | Result |
|------|--------|
| PC-A MAC address | [XX-XX-XX-XX-XX-XX] |
| OUI | [XX-XX-XX] |
| Serial number portion | [XX-XX-XX] |
| Vendor (IEEE OUI lookup) | [vendor name] |

### Step 2: S1 MAC addresses -where gotten using the 3 commands below

**`show interfaces vlan 1`**

- VLAN 1 status: [up/up]
- Hardware address: [xxxx.xxxx.xxxx]
- IP address: 192.168.1.2/24
- Switch OUI / vendor: [xx / Cisco]

**`show mac address-table`**

- PC-A's MAC learned dynamically on **F0/6** in VLAN 1: 
-
**`show arp`**


## Tools

Cisco Packet Tracer
## Key Takeaways

- Every Ethernet NIC has a unique, manufacturer-assigned MAC address (OUI + serial number).
- Switches learn source MAC addresses dynamically and map them to ports.
- ARP resolves IP addresses to MAC addresses, so the ARP and MAC address tables should agree.
