\# Macchanger and Wazuh Open Source SIEM



\## Project Overview



This cybersecurity project demonstrates MAC address randomization and restoration using Macchanger, along with service-level verification of the Wazuh Manager in a Kali Linux virtual machine running on VMware Workstation.



\## Project Objectives



\- Understand MAC addresses and network interface administration.

\- Randomize and restore a MAC address using Macchanger.

\- Manage Linux services using `systemctl`.

\- Inspect listening network ports using `ss`.

\- Understand the role of an open-source Security Information and Event Management (SIEM) platform.



\## Tools and Technologies



\- Kali Linux

\- VMware Workstation

\- Macchanger

\- Wazuh Manager

\- Linux networking utilities

\- `systemctl`

\- `ss`

\- `curl`

\- `ping`



\## Practical Implementation



\### 1. MAC Address Randomization



The practical involved checking the current and permanent MAC addresses, temporarily disabling the network interface, generating a randomized MAC address, verifying the change, and restoring the permanent address.



\### 2. Wazuh Manager Verification



The practical involved checking the Wazuh Manager service status and inspecting listening ports 1514, 1515, and 55000.



\### 3. Connectivity Check



A connectivity test was performed after the MAC address change. The recorded result was two replies from four packets, indicating 50% packet loss in that test.



\## Results and Limitations



\- MAC address randomization and restoration were demonstrated in the original lab.

\- The Wazuh Manager was reported as active.

\- Ports 1514, 1515, and 55000 were observed listening.

\- Wazuh API authentication was not successfully completed.

\- The Wazuh Indexer and Dashboard were not deployed.

\- Stable network connectivity was not established by the recorded ping test.

\- The original Kali Linux virtual machine was subsequently lost, so these practical tests have not been rerun in the current environment.



\## Project Documentation



\- \[Practical Project Report](docs/Macchanger\_Wazuh\_Project\_Report.pdf)

\- \[Project Analysis](docs/Macchanger\_Wazuh\_Project\_Analysis.pdf)



\## Learning Outcomes



\- Linux command-line operations

\- Network interface administration

\- MAC address randomization and restoration

\- Linux service management

\- Listening-port inspection

\- Introductory SIEM concepts



\## Ethical Use



This project was conducted for educational purposes in a personal virtual lab. MAC address changes and security monitoring should only be performed on systems and networks where authorization has been granted.

