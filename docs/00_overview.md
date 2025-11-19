# Digital Fortress Lab – Overview

This document provides a high‑level narrative overview of the Digital Fortress Lab: a self‑hosted security lab built on enterprise hardware and operated as a small production‑style environment. It expands on the information in the repository’s README and is intended for anyone who wants to understand how the lab is put together before diving into specific configurations or procedures.

## Goals

- **Realistic infrastructure:** Build a compact but realistic enterprise‑style network for experimentation and learning.
- **Integrated design:** Combine Proxmox virtualization, Dell storage, Cisco/SonicWall firewalls, and Suricata/SELKS into one coherent platform.
- **Visibility and control:** Use segmentation, firewall policy, and deep packet inspection to control and observe traffic flows.
- **Documented operations:** Keep enough documentation that the environment can be understood, changed, and rebuilt from scratch.

## Physical Platform (Summary)

| Component    | Description                                                                |
|--------------|----------------------------------------------------------------------------|
| **Compute**  | Dell PowerEdge R710 hosts most virtual machines; a pair of Dell EqualLogic FS7610 nodes provide additional compute and storage services. |
| **Storage**  | An Avid 18‑bay chassis populated with mixed SAS/SATA drives supplies bulk storage, while EqualLogic volumes present shared storage pools. |
| **Network**  | A Dell X1052P 52‑port switch acts as the core switching fabric. Dual shielded Cat6 patch panels organize cabling. An OpenGear console manager aggregates serial management ports, and a rack KVM provides local VGA/USB access. |
| **Security** | Cisco ASA 5510 and 5515‑X firewalls enforce perimeter policy, with a SonicWall SRA 4200 providing SSL VPN remote access. |
| **Monitoring** | A Panasonic Toughbook CF‑30 running NST/SELKS with Suricata serves as the SOC node for logging and traffic inspection. |

Further details on models and roles are documented in `docs/01_hardware-inventory.md`.

## Logical Architecture (Summary)

The lab is divided into several functional zones, each mapped to its own VLAN on the core switch and protected by firewall policy:

- **Management** – Switches, firewalls, console manager, lights‑out controllers, and the SOC node.
- **Core Services** – Proxmox nodes, storage appliances, and shared infrastructure services (e.g., directory, DNS, monitoring).
- **DMZ** – Public‑facing services for testing exposure and reverse proxy scenarios.
- **Lab** – General workloads and temporary experiments.
- **Honeypots** – Deliberately exposed services used to study scan and attack patterns in isolation.
- **Guest** – Untrusted devices and Wi‑Fi clients.

Routing between zones occurs on the firewalls, not on the switch. Selected traffic is mirrored into the Suricata/SELKS SOC node for inspection.

Additional details on VLAN IDs, addressing, and traffic flows are documented in `docs/02-network-architecture.md`. The associated diagram in the `diagrams/` folder provides a visual reference.