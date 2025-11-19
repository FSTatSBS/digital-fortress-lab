# Hardware Inventory

This document lists the main hardware components of the Digital Fortress Lab and the roles they play in the environment. Exact serial numbers, MAC addresses, and other unique identifiers are intentionally omitted.

---

## Rack Overview

The lab is built into a rack with structured cabling, patch panels, and out‑of‑band management. Devices are connected through the patch panels into the core switch, with console access centralized on the console manager and KVM.

---

## Compute and Virtualization

| Device                              | Key Specs                           | Role                                      |
|-------------------------------------|-------------------------------------|-------------------------------------------|
| Dell PowerEdge R710                 | Dual Xeon, 128 GB RAM              | Primary Proxmox virtualization host        |
| Dell EqualLogic FS7610 (Node 1)    | EqualLogic storage/controller node | Additional compute and storage services    |
| Dell EqualLogic FS7610 (Node 2)    | EqualLogic storage/controller node | Additional compute and storage services    |

The R710 hosts the bulk of the virtual machines. The FS7610 nodes are used to present shared storage and to host supporting services as needed.

---

## Storage

| Device                        | Bays / Media                                 | Role                                         |
|-------------------------------|----------------------------------------------|----------------------------------------------|
| Avid 18‑bay chassis           | Mixed SAS/SATA drives (user‑populated)      | Primary bulk storage for VMs and data        |
| EqualLogic FS7610 pair        | EqualLogic‑managed disk groups              | Shared storage for Proxmox and services      |

Drive sizes and exact layouts are documented in private notes; this repository focuses on the logical role of each chassis.

---

## Network and Management

| Device                           | Details                                        | Role                                     |
|----------------------------------|------------------------------------------------|------------------------------------------|
| Dell X1052P switch               | 52‑port managed switch                         | Core switching and VLAN hub              |
| Shielded Cat6 patch panels (×2)  | 24 ports each, pass‑through                    | Cable termination and cross‑connect      |
| OpenGear CM4148 console manager | 48‑port serial console server                  | Centralized serial/out‑of‑band access    |
| StarTech rack KVM               | 4‑port VGA/USB KVM                             | Direct access to selected rack devices   |
| HP TFT5600 rack console         | 15" LCD with keyboard and touchpad            | Local console for KVM and devices        |

Most copper links terminate at the patch panels, then run to the X1052P, keeping cabling predictable and serviceable.

---

## Security and Remote Access

| Device               | Details                                | Role                          |
|----------------------|----------------------------------------|-------------------------------|
| Cisco ASA 5510       | Hardware firewall appliance            | Perimeter firewall / policy   |
| Cisco ASA 5515‑X     | Hardware firewall appliance            | Perimeter firewall / policy   |
| SonicWall SRA 4200   | SSL VPN / remote‑access appliance      | Remote‑access gateway         |

ASA hardware originally arrived in a wiped state and was rebuilt and reintegrated into the lab with fresh policy and standardized management access.

---

## Monitoring / SOC Node

| Device                           | Details                                   | Role                                    |
|----------------------------------|-------------------------------------------|-----------------------------------------|
| Panasonic Toughbook CF‑30        | Rugged laptop running NST/SELKS stack     | Log sink, Suricata‑based SOC console    |

The SOC node receives logs and mirrored traffic from key points in the network and provides dashboards for inspection and analysis.

---

## Auxiliary / Experimental

| Device                                           | Details                | Role                                  |
|--------------------------------------------------|-----------------------|--------------------------------------|
| GL.iNet travel router (OpenWrt‑capable)          | Compact router         | Experimental routing / Wi‑Fi lab work |

Additional small devices may be added or removed over time for specific tests; the sections above cover the stable core of the lab.
