# Services and Virtual Machines

This document maps key services in the lab to the Proxmox virtual machines and physical hosts that provide them. It is a work in progress and will expand as the environment evolves.

## Core Infrastructure Services

| Service                          | Host / VM              | Notes                                   |
|---------------------------------|------------------------|-----------------------------------------|
| Directory Services              | (to be defined)        | LDAP/AD or equivalent                   |
| DNS / DHCP                      | (to be defined)        | Internal name resolution and addressing |
| NTP                             | (to be defined)        | Time synchronization for all nodes      |
| Log Aggregation & SOC           | Toughbook CF‑30 (physical) | NST/SELKS with Suricata and dashboards |
| Firewall & VPN                  | Cisco ASA / SonicWall   | Perimeter policy and remote access      |

## Security Services

| Service                          | Host / VM                   | Notes                                      |
|---------------------------------|-----------------------------|--------------------------------------------|
| Suricata/SELKS IDS/IPS          | Toughbook CF‑30 (physical)  | Deep packet inspection and alerting        |
| Log Collector / SIEM            | Toughbook CF‑30 (physical)  | Centralized logs and dashboards            |
| Honeypot Services               | Dedicated VMs in Honeypots zone | Exposed services for traffic analysis    |

## Application / Lab Workloads

The Lab zone hosts various test workloads and experiments. These VMs are created and torn down as needed.  
An updated list of active lab VMs will be added here over time.

## Honeypot Workloads

Honeypot VMs emulate vulnerable services and are deliberately exposed through the ASA. Examples might include:

- Web servers with outdated software
- SSH or FTP services with weak credentials
- Industrial control protocols or IoT devices

Specific honeypot configurations will be documented as they are deployed.

---

This document will evolve as services are defined and mapped. The current entries serve as placeholders and illustrate the intended structure.