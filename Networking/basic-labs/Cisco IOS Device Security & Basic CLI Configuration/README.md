# Cisco IOS Device Security & Basic CLI Configuration

## Objective
The objective of this project was to simulate an enterprise network environment by configuring fundamental device security and management settings on Cisco networking hardware. This lab focused on navigating the Cisco IOS Command-Line Interface (CLI), establishing secure privileged access, and managing configuration files to ensure infrastructure resilience.


## Network Topology
  <img width="575" height="369" alt="image" src="https://github.com/user-attachments/assets/715d3b2b-ae83-46ec-982d-fb2d3acd9158" />

## Project Steps

* **Step 1: Device Identification:** Navigated the Cisco IOS CLI and configured unique administrative hostnames for the router and switch from Global Configuration mode to ensure accurate device tracking.
  <img width="700" height="707" alt="image" src="https://github.com/user-attachments/assets/9e2c9b3f-e20a-49db-8bec-43225d02b255" />

* **Step 2: Access Control Configuration:** Established an initial `enable password` to restrict access to Privileged EXEC mode, preventing unauthorized users from altering the device configuration.
* 
  <img width="229" height="40" alt="image" src="https://github.com/user-attachments/assets/b22ae715-59f7-442e-87fe-04c323bcb75f" />

* **Step 3: Password Encryption:** Implemented the `service password-encryption` command to obscure clear-text passwords in the running configuration, providing a baseline layer of security (Type 7 encryption) against over-the-shoulder viewing.
  <img width="699" height="707" alt="image" src="https://github.com/user-attachments/assets/22feb485-6c31-40bc-86b5-9071b5c1ca5a" />

* **Step 4: Advanced Security Deployment:** Configured a more robust `enable secret` password. Verified through testing that the system correctly prioritizes this stronger, MD5-hashed (Type 5) encryption over the standard enable password.
  <img width="700" height="273" alt="image" src="https://github.com/user-attachments/assets/cba868e5-d24e-425a-82cd-613df286980a" />

* **Step 5: Configuration Management:** Committed the active `running-config` to the NVRAM `startup-config` (using `copy running-config startup-config` and `write memory`), ensuring that all critical security settings persist across device reboots and power cycles.
  <img width="333" height="221" alt="image" src="https://github.com/user-attachments/assets/fa3ff495-306a-466e-b28c-214db68e998d" />
  <img width="329" height="262" alt="image" src="https://github.com/user-attachments/assets/8c507574-7135-477e-82c7-34f41a3f1942" />


## Lessons Learned

* **CLI Navigation & Troubleshooting:** Gained hands-on experience moving efficiently through the Cisco IOS hierarchy (User EXEC, Privileged EXEC, and Global Configuration modes). This structural understanding is critical for quickly gathering device diagnostics and resolving connectivity issues in an IT Helpdesk or Analyst capacity.
* **Layered Network Security:** Developed a practical understanding of how to implement and verify different encryption standards on enterprise hardware, recognizing why relying solely on unencrypted or weakly encrypted passwords is a vulnerability.
* **Operational Best Practices:** Reinforced the crucial operational procedure of saving active configurations. Ensuring infrastructure configurations are persistent is a fundamental habit for maintaining network stability and supporting end-users effectively during outages.
