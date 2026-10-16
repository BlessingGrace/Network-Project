# Departmental Network Configuration and Access Control Using Cisco Packet Tracer

This project involves designing and configuring a departmental network using **Cisco Packet Tracer**. It demonstrates IP addressing, DHCP configuration, interdepartmental communication, and Access Control Lists (ACLs) to control network traffic between the IT, Sales, and HR departments.

## Table of Contents

- Project Overview
- Network Topology
- Tools and Technologies
- Configuration Steps
- Results and Findings
- Author

## Project Overview

This project aimed to design and implement a functional network infrastructure for three departments: **IT, Sales, and HR**.

The network was configured to enable communication between departments while applying access control policies to restrict specific traffic.

The main objectives were:

- Design a departmental network topology.
- Configure IP addressing for different departments.
- Implement DHCP to dynamically assign IP addresses.
- Configure routing to enable communication between departments.
- Implement Extended Access Control Lists (ACLs).
- Test network connectivity using ping.
- Verify FTP and HTTP access between departments.

## Network Topology

The network consists of three departmental networks connected through a central Cisco 2911 router.

Each department has its own Cisco 2960-24TT switch connecting its end devices.

**Network layout:**

- **IT Department:**
  - IT-PC1
  - IT-PC2
  - IT-Server0
  - ITSwitch
- **Sales Department:**
  - Sales-PC1
  - Sales-PC2
  - SalesSwitch
- **HR Department:**
  - HR-PC1
  - HR-PC2
  - HRSwitch
- **Central Device:**
  - Cisco 2911 Router (Router0)

**IP Addressing Scheme:**

| Department | Network Address | Subnet Mask   | Default Gateway |
| ---------- | --------------- | ------------- | --------------- |
| IT         | 192.168.10.0    | 255.255.255.0 | 192.168.10.1    |
| Sales      | 192.168.20.0    | 255.255.255.0 | 192.168.20.1    |
| HR         | 192.168.30.0    | 255.255.255.0 | 192.168.30.1    |

The HR-PC1 configuration screenshot shows the following assigned settings:

- **IP Address:** 192.168.30.2
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** 192.168.30.1
- **Address Assignment:** DHCP

## Tools and Technologies

- **Cisco Packet Tracer 9.0.1:** Network design, configuration, and simulation.
- **Cisco 2911 Router:** Interdepartmental routing and traffic control.
- **Cisco 2960-24TT Switches:** Departmental network connectivity.
- **End Devices:** PCs and a server.
- **DHCP:** Dynamic IP address allocation.
- **Extended ACLs:** Network traffic filtering and access control.
- **Cisco IOS CLI:** Router configuration and verification.
- **Ping:** Network connectivity testing.
- **FTP:** File transfer connectivity testing.
- **HTTP:** Web service connectivity testing.

## Configuration Steps

### 1. Network Topology Design

1. Open Cisco Packet Tracer.
2. Add one Cisco 2911 router.
3. Add three Cisco 2960-24TT switches.
4. Add the required PCs and server for each department.
5. Connect each department's devices to its corresponding switch.
6. Connect all three switches to the central router.

### 2. IP Address Configuration

Configure the departmental networks using the following addressing scheme:

- IT: `192.168.10.0/24`
- Sales: `192.168.20.0/24`
- HR: `192.168.30.0/24`

Configure the corresponding default gateways:

- IT: `192.168.10.1`
- Sales: `192.168.20.1`
- HR: `192.168.30.1`

### 3. DHCP Configuration

Configure DHCP on the router to dynamically assign IP addresses to devices in each department.

The following commands were used:

```
enable
configure terminal

ip dhcp excluded-address 192.168.10.1 192.168.10.2

ip dhcp pool IT_POOL
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
exit

ip dhcp pool SALES_POOL
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
exit

ip dhcp pool HR_POOL
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
exit
```

### 4. Extended ACL Configuration

An Extended Access Control List named `Sales-ACL` was configured to restrict ICMP traffic from the Sales network to the IT network while allowing other IP traffic.

The following commands were used:

```
ip access-list extended Sales-ACL
deny icmp 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
permit ip any any
exit
```

Apply the ACL to the router interface:

```
interface gigabitEthernet 0/1
ip access-group Sales-ACL in
exit
```

Verify the ACL configuration:

```
show access-lists
```

### 5. Network Connectivity Testing

Use the `ping` command from departmental PCs to verify network connectivity.

Test the following:

1. Sales to HR connectivity.
2. Sales to IT connectivity.
3. HR to IT connectivity.
4. HR to Sales connectivity.
5. IT to HR connectivity.

### 6. FTP and HTTP Testing

Test application-level connectivity between the Sales and IT departments.

- Verify FTP access from Sales to IT.
- Verify HTTP access from Sales to IT.

## Results and Findings

The network configuration and connectivity tests produced the following results:

| Source | Destination | Test | Result     |
| ------ | ----------- | ---- | ---------- |
| Sales  | HR          | Ping | Successful |
| Sales  | IT          | Ping | Blocked    |
| Sales  | IT          | FTP  | Allowed    |
| Sales  | IT          | HTTP | Allowed    |
| HR     | IT          | Ping | Successful |
| HR     | Sales       | Ping | Successful |
| HR     | IT          | FTP  | Allowed    |
| IT     | HR          | Ping | Successful |

**Key Findings:**

- The three departmental networks were successfully connected through the central router.
- DHCP pools were configured for IT, Sales, and HR.
- The Extended ACL successfully restricted ICMP traffic from Sales to IT.
- Other IP traffic was permitted through the `permit ip any any` statement.
- FTP and HTTP access from Sales to IT remained allowed.
- Connectivity between HR and the other departments was successfully demonstrated.
- The `show access-lists` command confirmed that the ACL was configured on the router.

**Conclusion:**

This project provided practical experience in network design, IP addressing, DHCP configuration, routing, and access control using Cisco Packet Tracer. It demonstrated how Extended ACLs can be used to implement network security policies while maintaining access to permitted network services.

## Author

**Blessing Oyeniran**

- **Field:** Computer Science, Networking, and Cybersecurity

**Professional Interests:** Network Engineering, Cybersecurity, Network Security, and IT Infrastructure.

