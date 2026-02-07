# \# Security Operations Center Lab





\## Summary



This project simulates a real-world cyberattack lifecycle to engineer a robust defense system. I deployed a Security Information and Event Management (SIEM) solution within a segmented home lab environment to monitor, detect, and analyze live threats.



The lab demonstrates an end-to-end security workflow:

1\.  \*\*Infrastructure:\*\* Establishing a Zero-Trust mesh network.

2\.  \*\*Offense (Red Team):\*\* Executing controlled brute-force attacks.

3\.  \*\*Defense (Blue Team):\*\* Analyzing logs and configuring automated alerts.



\## Project Modules



| Module | Description | Key Tech |

| :--- | :--- | :--- |

| \[\*\*01-Infrastructure\*\*](./01-infrastructure) | \*\*Network Engineering:\*\* Secure mesh networking, VM provisioning, and segmentation. | Proxmox, Tailscale, Ubuntu |

| \[\*\*02-Offensive Ops\*\*](./02-offensive-ops) | \*\*Red Team Simulation:\*\* Service enumeration and automated dictionary attacks (Hydra). | Kali Linux, Nmap, Hydra |

| \[\*\*03-Defensive Ops\*\*](./03-defensive-ops) | \*\*Blue Team Analysis:\*\* Log ingestion, threat correlation, and forensic investigation. | Wazuh, Docker, Syslog |



---



\## Network Topology

The environment utilizes Tailscale to create an encrypted overlay network, isolating the lab from the physical home LAN.



```mermaid

graph TD

&nbsp;   subgraph Proxmox\_Host \["🖥️ Proxmox Host (Home Lab)"]

&nbsp;       direction TB

&nbsp;       

&nbsp;       subgraph VM\_Attacker \["🔴 Red Team (Kali)"]

&nbsp;           Kali\[Attacker Node]

&nbsp;           IP\_Kali\["IP: 100.x.x.1"]

&nbsp;       end

&nbsp;       

&nbsp;       subgraph VM\_Target \["🟢 Target (Ubuntu)"]

&nbsp;           Ubuntu\[Web Server]

&nbsp;           Agent\[Wazuh Agent]

&nbsp;           IP\_Ubu\["IP: 100.x.x.2"]

&nbsp;       end

&nbsp;       

&nbsp;       subgraph VM\_Defense \["🔵 Blue Team (SIEM)"]

&nbsp;           Wazuh\[Wazuh Manager]

&nbsp;           Docker\[Docker Container]

&nbsp;           IP\_Waz\["IP: 100.x.x.3"]

&nbsp;       end

&nbsp;   end

&nbsp;   

&nbsp;   %% Traffic Flow

&nbsp;   Kali -.->|SSH Brute Force| Ubuntu

&nbsp;   Ubuntu ==>|Log Shipping (Port 1514)| Wazuh

```



\## Technologies



Hypervisor: Proxmox VE



SIEM: Wazuh



Networking: Tailscale



Tools: Nmap, Hydra, Docker, Linux



\## Disclaimer



This project is for educational purposes only. All attacks were simulated in a controlled, isolated environment owned by the author.

