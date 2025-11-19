# Digital Fortress Lab

**Digital Fortress Lab** is a self-hosted security and infrastructure lab built on enterprise hardware and operated like a small production network.

It combines:

- Proxmox virtualization
- Dell server and storage platforms
- Cisco ASA and SonicWall security appliances
- VLAN-based segmentation on a managed switch
- Centralized logging and IDS/IPS with NST/SELKS and Suricata

The lab is isolated from production networks and is used to design, test, and operate realistic network and security topologies.

---

## 📌 Quick Facts

| Item             | Description                                                     |
|------------------|-----------------------------------------------------------------|
| Environment type | Self-hosted, isolated security & infrastructure lab            |
| Core hypervisor  | Proxmox VE on Dell PowerEdge R710                               |
| Storage          | EqualLogic FS7610 (2 nodes) + Avid 18-bay storage chassis       |
| Switching        | Dell X1052P managed switch + dual shielded patch panels         |
| Perimeter        | Cisco ASA 5510 / 5515-X + SonicWall SRA 4200                    |
| Monitoring       | Panasonic Toughbook CF-30 running NST/SELKS + Suricata          |
| Network model    | Multi-VLAN, zone-based segmentation with ASA as L3 boundary     |

---

## 🗺️ Table of Contents

- [Purpose](#-purpose)
- [Physical Platform](#-physical-platform)
  - [Core Hardware Summary](#core-hardware-summary)
  - [Hardware Gallery](#hardware-gallery)
- [Logical Architecture](#-logical-architecture)
  - [Zones](#zones-sanitized)
  - [Traffic Flows](#traffic-flows-conceptual)
  - [Addressing Approach](#addressing-approach-sanitized)
- [Security & Monitoring](#-security--monitoring)
- [Repository Layout](#-repository-layout)
- [Operations Model](#-operations)
- [Sanitization & Scope](#-sanitization--scope)

---

## 🧭 Purpose

The lab is intended to:

- Model a compact, enterprise-style network end to end  
- Provide a controlled environment for:
  - Firewall policy and access control  
  - VPN and remote access scenarios  
  - Segmentation and exposure tests  
- Capture logs and packet data for:
  - IDS/IPS analysis and tuning  
  - Investigating traffic patterns and attack behavior  
- Practice routine operations:
  - Backup and restore  
  - Change management  
  - Incremental topology changes

This repository documents:

- The **physical layout** of the rack
- The **logical design** of networks and zones
- The **security model** and monitoring approach
- The **operations model** used to keep the lab coherent over time

---

## 🧱 Physical Platform

The environment is built into a rack with structured cabling, patch panels, and out-of-band access.

### Core Hardware Summary

| Category              | Components                                                                                     | Role                                                       |
|-----------------------|------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| Compute               | Dell PowerEdge R710 (dual Xeon, 128 GB RAM)                                                   | Primary Proxmox host                                       |
| Additional Compute    | Dell EqualLogic FS7610 (2 nodes)                                                              | Storage/services appliance; additional compute capability  |
| Storage               | Avid 18-bay chassis with mixed SAS/SATA disks                                                | Bulk and lab storage                                       |
| Switching             | Dell X1052P 52-port managed switch                                                            | Core switching and VLAN hub                                |
| Cabling               | Dual shielded Cat6 patch panels (front + rear)                                               | Cable termination and cross-connect                        |
| Out-of-band access    | OpenGear CM4148 console manager, rackmount KVM, HP TFT5600 rack console                      | Serial and local VGA/keyboard access                       |
| Security appliances   | Cisco ASA 5510 / 5515-X, SonicWall SRA 4200                                                   | Perimeter firewalling, zone routing, and VPN               |
| Monitoring / SOC node | Panasonic Toughbook CF-30 running NST/SELKS with Suricata                                    | Central logging, DPI, and alerting                         |

All devices are cabled through the patch panels into the core switch.  
Management access is available over:

- A dedicated **management VLAN**
- **Serial console** via OpenGear CM4148
- Local **KVM / rack console**

---

### Hardware Gallery

> Images are illustrative and correspond to the actual lab hardware.  
> Click to expand each category.

<details>
  <summary><strong>Compute</strong> – Proxmox host and EqualLogic nodes</summary>

- Dell PowerEdge R710 – primary Proxmox host  
  ![](/assets/photos/Compute1.jpg)

- Dell EqualLogic FS7610 (2 nodes) – additional compute and storage  
  ![](/assets/photos/Compute2.png)

</details>

<details>
  <summary><strong>Storage</strong> – Avid chassis and EqualLogic storage</summary>

- Avid 18-bay chassis with mixed SAS/SATA disks  
  ![18-bay chassis](/assets/photos/Storage1.png)

- EqualLogic-backed storage presented to Proxmox and other services  
  ![backed storage presented to Proxmox and other services](/assets/photos/Storage2.png)

</details>

<details>
  <summary><strong>Network & Management</strong> – Switch, patch panels, console access</summary>

- Dell X1052P 52-port managed switch – core switching and VLAN hub  
  ![core switching and VLAN hub](/assets/photos/switch.jpg)

- Dual shielded Cat6 patch panels (front + rear) – cable termination and cross-connect  
  ![patch panels](/assets/photos/patch.jpg)

- OpenGear CM4148 console manager – centralized serial access for network and security devices  
  ![console manager](/assets/photos/console3.jpg)

- Rackmount KVM and HP TFT5600 rack console – local VGA/keyboard access  
  ![local VGA/keyboard access](/assets/photos/console1.jpg)  
  ![local VGA/keyboard access](/assets/photos/console2.jpg)

</details>

<details>
  <summary><strong>Security & Monitoring</strong> – Firewalls, VPN, SOC node</summary>

- Cisco ASA 5510 / 5515-X – perimeter firewalls and zone routing  
  ![perimeter firewalls and zone routing](/assets/photos/sec1.jpg)  
  ![perimeter firewalls and zone routing](/assets/photos/sec3.jpg)

- SonicWall SRA 4200 – SSL VPN and remote access gateway  
  ![SSL VPN and remote access gateway](/assets/photos/sec2.jpg)

- Panasonic Toughbook CF-30 – NST/SELKS and Suricata SOC node  
  ![NST/SELKS and Suricata as a small SOC node](/assets/photos/monitor1.jpg)  
  ![NST/SELKS and Suricata as a small SOC node](/assets/photos/monitor2.jpg)

</details>

---

## 🌐 Logical Architecture

The network is segmented into distinct zones. Each zone maps to one or more VLANs on the Dell X1052P and to specific policies on the ASA.

### Zones (Sanitized)

| Zone        | Role                                              |
|------------|---------------------------------------------------|
| Management | Switch, firewalls, console, iDRAC, SOC node       |
| Core       | Proxmox host(s), storage, shared infrastructure   |
| DMZ        | Externally reachable lab services                 |
| Lab        | General-purpose workloads and test VMs            |
| Honeypots  | Intentionally exposed services for observation    |
| Guest      | Untrusted devices and temporary clients           |

The Dell X1052P switch provides **Layer 2 separation** for each VLAN.  
**Inter-VLAN routing and filtering** are performed on the ASA, not on the switch.

---

### Traffic Flows (Conceptual)

| Flow                         | Purpose                                           | Controls                                                |
|------------------------------|---------------------------------------------------|---------------------------------------------------------|
| Internet ↔ ASA ↔ DMZ         | Public-facing services and exposure tests        | ASA ACLs, NAT, logging                                  |
| Internet ↔ ASA/SRA ↔ Mgmt    | Remote administration over VPN                   | VPN profiles, restricted subnets, authentication        |
| Lab / Guest ↔ ASA ↔ Internet | Outbound access for tools and clients            | Restricted egress rules, logging                        |
| Honeypots ↔ ASA ↔ Internet   | Inbound scans/attacks to honeypot zone           | Controlled inbound; tightly limited outbound            |
| Mgmt ↔ Other zones           | Admin access to infrastructure                   | Protocol + host-specific ACLs on ASA                    |

Exact IP addressing and VLAN IDs are documented in sanitized form in:

- `docs/02-network-architecture.md`

---

### Addressing Approach (Sanitized)

- Each zone uses a **distinct RFC1918 subnet** (for example, `/24` ranges per zone).
- The **ASA is the default gateway** for all VLANs.
- The Dell X1052P operates in **L2 mode only** (no L3 SVIs used for routing).
- Management IPs for infrastructure (switch, firewalls, iDRAC, console, SOC node) live exclusively in the **Management subnet**.
- Public address examples and NAT mappings use **documentation ranges** only (e.g., `198.51.100.0/24`, `203.0.113.0/24`).

---

## 🔒 Security & Monitoring

Security and observability are part of the base design, not an afterthought.

### Perimeter & Segmentation

**Cisco ASA appliances:**

- Define interface roles:
  - `outside`, `management`, `core`, `dmz`, `lab`, `honeypots`, `guest`
- Apply NAT rules:
  - Public-facing services in the DMZ
  - Outbound access from lab, guest, and honeypot zones
- Enforce ACLs that:
  - Explicitly permit required inter-zone traffic
  - Deny and log everything else by default

**SonicWall SRA 4200:**

- Terminates remote VPN sessions
- Exposes only:
  - Selected management subnets
  - Optional lab subnets for remote work
- Uses authentication and restricted routing to avoid broad access

Administrative interfaces for core infrastructure devices are reachable **only** from the management zone.

---

### Logging, DPI, and SOC Node

The Toughbook CF-30, running NST/SELKS (including Suricata), acts as a compact SOC node.

It:

- Receives:
  - Syslog from ASA and SonicWall
  - Logs from selected hosts and core services
  - Mirrored traffic from key switch ports and/or ASA interfaces
- Provides:
  - Deep packet inspection with Suricata
  - Dashboards and alert views through the SELKS stack

Monitoring design focuses on a limited set of well-chosen mirror points:

- Example: DMZ ↔ Internet, Honeypots ↔ Internet  
- Goal: capture **high-value** traffic paths rather than all traffic

Additional detail is documented in:

- `docs/03-security-architecture.md`

---

## 📁 Repository Layout

The repository mirrors the structure of the lab and its documentation.

```text
digital-fortress-lab/
├── README.md
├── docs/
│   ├── 00_overview.md
│   ├── 01_hardware-inventory.md
│   ├── 02-network-architecture.md
│   ├── 03-security-architecture.md
│   ├── 04-services-and-vms.md
│   ├── 05-operations-and-maintenance.md
│   └── 06-future-roadmap.md
├── diagrams/
│   └── logical-network-diagram.png
├── infra/
│   ├── example-firewall-policies/
│   │   └── asa-lab-base-policy.txt
│   ├── sample-ansible-playbooks/
│   └── scripts/
├── runbooks/
│   └── change-log.md
└── assets/
    └── photos/
```

### How to Navigate

- Start with: `docs/00_overview.md` – narrative overview of the lab
- Then: `docs/02-network-architecture.md` – network layout, VLANs, and flows
- And: `docs/03-security-architecture.md` – security model and monitoring

---

## ⚙️ Operations

The lab is operated with the expectation that it will evolve and occasionally be rebuilt.

- **Backups**
  - Device configurations and Proxmox VM backups are taken regularly (stored outside this repository).
  - Backup and restore procedures are tracked under `docs/05-operations-and-maintenance.md`.

- **Change Tracking**
  - Topology and policy changes are reflected in the relevant `docs/` files.
  - Each significant change is summarized in `runbooks/change-log.md`.

- **Experiments**
  - New services, exposure tests, or honeypot configurations are:
    - Introduced in the lab
    - Documented so the logical design stays aligned with reality

The goal is for the lab to remain understandable and reproducible rather than drifting into an ad-hoc configuration.

---

## 🧼 Sanitization & Scope

All content in this repository is intentionally sanitized:

- IP ranges, hostnames, and network object names are **examples**, not live values.
- No keys, credentials, VPN profiles, or other secrets are committed.
- Hardware identifiers such as serial numbers and MAC addresses are omitted.
- Configuration examples (such as `asa-lab-base-policy.txt`) are **structural** only and cannot be applied 1:1 to any real environment.

The lab is isolated from any production or customer systems.  
Honeypot and exposure testing is confined to this environment and configured to avoid unintended impact on external networks.

---
