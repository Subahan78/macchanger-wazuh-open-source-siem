# Practical Commands Guide: Macchanger and Wazuh SIEM

## Project Information

| Item | Details |
|---|---|
| Project | Macchanger and Wazuh Open Source SIEM |
| Operating System | Kali Linux |
| Virtualization | VMware Workstation |
| Network Interface | `eth0` |
| MAC Address Utility | Macchanger |
| Security Monitoring | Wazuh Manager |
| Project Team ID | PTID-CSPP-AUG-26-540 |

## 1. Project Overview

This guide documents Linux commands used in a cybersecurity lab to manage a network interface, randomize and restore its MAC address, inspect Linux service status, and examine listening ports associated with Wazuh.

The commands are documented for learning and reference. The original Kali Linux virtual machine was subsequently lost, so the lab has not been rerun in the current environment.

## 2. Network Interface Fundamentals

A network interface connects a system to a network. Linux provides command-line utilities to inspect and manage interfaces.

### 2.1 Identify network interfaces

```bash
ip link show
```

**Purpose:** Lists network interfaces and their current state.

### 2.2 Inspect IP addressing

```bash
ip addr show
```

**Purpose:** Displays interface details, IP addresses, and interface state.

### 2.3 Inspect the routing table

```bash
ip route
```

**Purpose:** Displays configured network routes, including the default route when present.

## 3. MAC Address Management with Macchanger

A MAC address is a link-layer identifier associated with a network interface. Macchanger can display and change the address exposed by a supported interface.

### 3.1 Check the current and permanent MAC addresses

```bash
sudo macchanger -s eth0
```

**Purpose:** Displays the current and permanent MAC address information reported for `eth0`.

### 3.2 Disable the interface

```bash
sudo ip link set eth0 down
```

**Purpose:** Temporarily disables the interface before changing its MAC address.

### 3.3 Generate a randomized MAC address

```bash
sudo macchanger -r eth0
```

**Purpose:** Requests a randomized MAC address for the interface.

### 3.4 Re-enable the interface

```bash
sudo ip link set eth0 up
```

**Purpose:** Brings the interface back up.

### 3.5 Verify the change

```bash
sudo macchanger -s eth0
```

Compare the reported current MAC address with the permanent address.

### 3.6 Restore the permanent MAC address

```bash
sudo ip link set eth0 down
sudo macchanger -p eth0
sudo ip link set eth0 up
sudo macchanger -s eth0
```

**Purpose:** Disables the interface, requests restoration of its permanent MAC address, brings the interface up, and checks the reported result.

**Important:** Interface names, permissions, driver support, and network configuration can affect these operations. Changing a MAC address may interrupt connectivity. Use an authorized lab interface and verify the result rather than assuming the command succeeded.

## 4. Wazuh Manager Service Management

Wazuh is an open-source security monitoring platform. Its Manager processes security data and supports security event analysis.

### 4.1 Check the service status

```bash
sudo systemctl status wazuh-manager --no-pager
```

**Purpose:** Displays the Wazuh Manager service state without opening an interactive pager.

Look for the `Active:` field. An `active (running)` state indicates that the service is running; it does not by itself prove that every Wazuh component is configured correctly.

### 4.2 Check service activity

```bash
systemctl is-active wazuh-manager
```

**Purpose:** Provides a concise service-state result, such as `active` or `inactive`.

### 4.3 Review recent service logs

```bash
sudo journalctl -u wazuh-manager -n 50 --no-pager
```

**Purpose:** Displays recent journal entries for troubleshooting the service.

If the service fails, review the logs before attempting configuration changes.

## 5. Inspect Listening Ports

The `ss` utility displays socket information and is useful when investigating which network ports are listening.

### 5.1 Inspect the ports used in this project

```bash
sudo ss -lntp | grep -E '1514|1515|55000'
```

**Options explained:**

- `-l`: Display listening sockets.
- `-n`: Display numeric addresses and ports.
- `-t`: Display TCP sockets.
- `-p`: Display process information when available.
- `grep -E`: Filter output using an extended regular expression.

### 5.2 Understand the relevant Wazuh ports

| Port | Typical purpose |
|---|---|
| `1514` | Wazuh agent communication |
| `1515` | Wazuh agent enrollment |
| `55000` | Wazuh API |

Actual availability depends on the installation, configuration, and service state. A listening port alone does not prove that an end-to-end workflow is working.

## 6. Basic Network Connectivity Troubleshooting

### 6.1 Test connectivity to a hostname

```bash
ping -c 4 google.com
```

**Purpose:** Sends four ICMP echo requests to test connectivity and name resolution together.

### 6.2 Interpret the result

Review the number of packets transmitted, received, and lost.

- Replies indicate that echo responses were received.
- Packet loss indicates that some requests did not receive replies.
- No replies do not necessarily prove that the destination is offline; ICMP traffic may be filtered.

**Recorded lab result:** The original report recorded two replies from four packets, corresponding to 50% packet loss in that test. This does not establish stable connectivity.

## 7. Troubleshooting Reference

| Symptom | What to investigate |
|---|---|
| Interface not found | Run `ip link show` and verify the interface name |
| MAC address change fails | Check privileges, interface state, and driver support |
| Connectivity is interrupted | Check `ip addr show`, `ip route`, and interface state |
| Wazuh Manager is inactive | Inspect `systemctl status` and the service journal |
| Expected port is missing | Check the service state and configuration |
| Wazuh API returns Unauthorized | Verify API credentials and authentication configuration through authorized procedures |

These are troubleshooting suggestions, not claims that each issue was reproduced during this project.

## 8. Recorded Results and Limitations

The existing project report documents the following:

- MAC address randomization and restoration were performed in the original lab.
- The Wazuh Manager was reported as active.
- Ports `1514`, `1515`, and `55000` were observed listening.
- Wazuh API authentication was unsuccessful.
- The Wazuh Indexer and Dashboard were not deployed.
- The recorded connectivity test showed 50% packet loss.
- The original Kali Linux virtual machine was subsequently lost, and the practical has not been rerun.

The project therefore demonstrates introductory Linux networking and Wazuh Manager administration. It does not establish a fully deployed SIEM monitoring pipeline or a completed alert-detection workflow.

## 9. Skills Demonstrated

- Linux command-line administration
- Network interface inspection and management
- MAC address randomization and restoration
- Linux service management using `systemctl`
- Socket and port inspection using `ss`
- Basic connectivity troubleshooting
- Introductory SIEM concepts
- Technical documentation and troubleshooting analysis

## 10. Ethical and Safe Use

Perform network changes and security testing only on systems and networks you own or are explicitly authorized to administer. Do not use MAC address changes to bypass access controls or impersonate other devices.

## Related Project Documentation

- [Project Report](Macchanger_Wazuh_Project_Report.pdf)
- [Project Analysis](Macchanger_Wazuh_Project_Analysis.pdf)
