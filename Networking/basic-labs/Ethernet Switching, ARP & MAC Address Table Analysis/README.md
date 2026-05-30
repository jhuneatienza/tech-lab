# Ethernet Switching, ARP & MAC Address Table Analysis

## Objective
The objective of this project was to analyze Layer 2 Ethernet switching operations by simulating network traffic, observing Address Resolution Protocol (ARP) behavior, and examining how Cisco switches dynamically build and manage their MAC Address tables. This lab reinforces core understanding of unicast and broadcast traffic flow across a local area network.

## Network Topology
<img width="965" height="396" alt="Topology" src="https://github.com/user-attachments/assets/885644c2-bc07-4f13-bef1-49ebfbaed999" />


## Project Steps

* **Step 1: Traffic Simulation & ARP Observation:** Initiated ICMP traffic (ping) between end hosts (PCs) on the network. Observed how the initial communication requires an ARP Request (a broadcast message to all local devices) to discover the destination MAC address before the ICMP Echo Request can be sent.
* **Step 2: Packet Analysis:** Used simulation mode to analyze network frames. Inspected the outbound Protocol Data Unit (PDU) details, verifying key Ethernet frame fields such as the Destination MAC (e.g., the `FFFF.FFFF.FFFF` broadcast address), Source MAC, and the Ethernet Type field (`0x0806` for ARP).
  <img width="939" height="457" alt="image" src="https://github.com/user-attachments/assets/d65cec0c-d4e9-4292-a13d-5d773b58d957" />
  
        **Step 2.1 - Communication Initiation:** PC1 (192.168.1.1) attempts to ping PC3 (192.168.1.3). Because its ARP table is empty, PC1 buffers the ICMP packet and prepares an ARP Request to discover PC3's MAC address.
  <img width="977" height="394" alt="image" src="https://github.com/user-attachments/assets/e43e55ff-d52b-4c94-9636-e08d78c4cd49" />
  
        **Step 2.2 - ARP Broadcast (Switch 1):** PC1 sends the ARP Request to Switch 1 (SW1). Recognizing the destination MAC as a broadcast address (FFFF.FFFF.FFFF), SW1 floods the frame out all active ports. PC2 receives the frame but drops it (indicated by the red X) because the target IP does not match its own.
  <img width="1037" height="434" alt="image" src="https://github.com/user-attachments/assets/8dedcf9b-7280-43dc-a31c-af38cc12d028" />
  
        **Step 2.3 - ARP Broadcast (Switch 2):** The broadcast frame travels over the inter-switch link to Switch 2 (SW2), which also floods it out to its connected hosts. PC4 drops the packet, but PC3 accepts it because the target IP address matches.
  <img width="969" height="380" alt="image" src="https://github.com/user-attachments/assets/e6a3ee61-4386-45cf-97de-7da65e67a366" />
  
        **Step 2.4 - ARP Reply Generation:** PC3 processes the ARP Request and generates an ARP Reply. Unlike the request, this reply is a unicast frame addressed specifically to PC1's MAC address.
  <img width="1052" height="409" alt="image" src="https://github.com/user-attachments/assets/cca354a0-dbfb-4549-a1ec-7a151af9ab38" />
  
        **Step 2.5 - Unicast Forwarding:** The unicast ARP Reply travels from PC3 to SW2, and then across the link to SW1. The switches use their dynamically built MAC address tables to forward the frame directly, rather than broadcasting it.
  <img width="972" height="403" alt="image" src="https://github.com/user-attachments/assets/f8998702-1a5a-4402-a6cb-877388224ef3" />
  
        **Step 2.6 - ARP Resolution Complete:** SW1 forwards the unicast ARP Reply directly to PC1. PC1 updates its ARP table with PC3's MAC address and can now successfully send the original ICMP Echo Request (ping).
  






* **Step 3: Generating Network Traffic:** Generated cross-network traffic between all simulated client endpoints to populate the dynamic MAC address tables of the interconnecting switches.
  <img width="702" height="709" alt="Step 3 1" src="https://github.com/user-attachments/assets/f16efe48-b505-4283-be6f-721be3fe4e19" />
  <img width="696" height="702" alt="Step 3 2" src="https://github.com/user-attachments/assets/4fb2d36d-5234-46cd-b180-4e584cec9480" />


* **Step 4: MAC Address Table Verification:** Navigated to Privileged EXEC mode on the switches and utilized the `show mac address-table` command. Correlated the dynamically learned MAC addresses to their respective switch port interfaces (e.g., FastEthernet0/1, GigabitEthernet0/1) to identify exactly which host lived on which port.

  
  <img width="439" height="183" alt="Step 4 1" src="https://github.com/user-attachments/assets/e9330b9f-3464-4122-9a8c-2636df148997" />
  <img width="337" height="186" alt="Step 4 2" src="https://github.com/user-attachments/assets/98737815-ac09-45b4-8a16-124f8318d499" />

  
* **Step 5: Table Management:** Executed the `clear mac address-table dynamic` command to flush the dynamically learned entries from the switches, demonstrating how to manually force a switch to re-learn network topologies.
  <img width="645" height="162" alt="Step 5 1" src="https://github.com/user-attachments/assets/662b8902-91df-4462-a4b5-a9949b1a38cd" />
  <img width="423" height="156" alt="Step 5 2" src="https://github.com/user-attachments/assets/bc424ef0-0df1-4528-a14b-dea091066e16" />


## Lessons Learned

* **Layer 2 Traffic Flow:** Solidified a deep understanding of how switches handle different traffic types. Specifically, how broadcast traffic (like an ARP Request) is flooded out all ports except the receiving port, while unicast traffic (like an ARP Reply or ICMP ping) is forwarded only to the specific port associated with the destination MAC.
* **Switch Forwarding Logic:** Gained practical insight into how a Cisco switch dynamically builds its MAC address table by inspecting the Source MAC address of incoming frames.
* **Network Troubleshooting Foundations:** Tracing MAC addresses to specific interfaces is a crucial Helpdesk and Network Admin skill. Learning how to correlate a MAC address from a specific switch port is often the first step in locating a problematic device, resolving an IP conflict, or verifying connectivity on an enterprise network floor.
