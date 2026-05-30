# Ethernet Switching, ARP & MAC Address Table Analysis

## Objective
The objective of this project was to analyze Layer 2 Ethernet switching operations by simulating network traffic, observing Address Resolution Protocol (ARP) behavior, and examining how Cisco switches dynamically build and manage their MAC Address tables. This lab reinforces core understanding of unicast and broadcast traffic flow across a local area network.

## Project Steps

* **Step 1: Traffic Simulation & ARP Observation:** Initiated ICMP traffic (ping) between end hosts (PCs) on the network. Observed how the initial communication requires an ARP Request (a broadcast message to all local devices) to discover the destination MAC address before the ICMP Echo Request can be sent.
* **Step 2: Packet Analysis:** Used simulation mode to analyze network frames. Inspected the outbound Protocol Data Unit (PDU) details, verifying key Ethernet frame fields such as the Destination MAC (e.g., the `FFFF.FFFF.FFFF` broadcast address), Source MAC, and the Ethernet Type field (`0x0806` for ARP).
* **Step 3: Generating Network Traffic:** Generated cross-network traffic between all simulated client endpoints to populate the dynamic MAC address tables of the interconnecting switches.
* **Step 4: MAC Address Table Verification:** Navigated to Privileged EXEC mode on the switches and utilized the `show mac address-table` command. Correlated the dynamically learned MAC addresses to their respective switch port interfaces (e.g., FastEthernet0/1, GigabitEthernet0/1) to identify exactly which host lived on which port.
* **Step 5: Table Management:** Executed the `clear mac address-table dynamic` command to flush the dynamically learned entries from the switches, demonstrating how to manually force a switch to re-learn network topologies.

## Lessons Learned

* **Layer 2 Traffic Flow:** Solidified a deep understanding of how switches handle different traffic types. Specifically, how broadcast traffic (like an ARP Request) is flooded out all ports except the receiving port, while unicast traffic (like an ARP Reply or ICMP ping) is forwarded only to the specific port associated with the destination MAC.
* **Switch Forwarding Logic:** Gained practical insight into how a Cisco switch dynamically builds its MAC address table by inspecting the Source MAC address of incoming frames.
* **Network Troubleshooting Foundations:** Tracing MAC addresses to specific interfaces is a crucial Helpdesk and Network Admin skill. Learning how to correlate a MAC address from a specific switch port is often the first step in locating a problematic device, resolving an IP conflict, or verifying connectivity on an enterprise network floor.
