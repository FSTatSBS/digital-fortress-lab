# Digital Fortress Lab

**Digital Fortress Lab** is a self-hosted security lab built on enterprise hardware and operated as a small production-style environment.  
It combines Proxmox virtualization, Dell storage, Cisco ASA and SonicWall firewalls, VLAN segmentation, deep packet inspection, and a Suricata/SELKS SOC node into a single, coherent platform for network and security engineering work.

---

## 1. Purpose and Scope

The lab is designed to behave like a compact enterprise network rather than a casual homelab. It provides a controlled environment to:

- Run virtualized workloads on realistic hardware
- Design and refine network segmentation and firewall policies
- Collect and inspect traffic with IDS/IPS and centralized logging
- Practice backup, recovery, and change management procedures

This repository holds the **documentation, diagrams, and sanitized configuration examples** that describe how the environment is assembled and operated. It does *not* contain live secrets or full device configurations.

---

## 2. Physical Platform

The lab is built into a rack with structured cabling and out‑of‑band access, so that every device can be serviced without rearranging hardware.

### 2.1 Core Hardware

| Layer        | Components                                                                                | Role                                                         |
|-------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| Compute     | Dell PowerEdge R710 (dual Xeon, 128 GB RAM), Dell EqualLogic FS7610 (2 nodes)               | Primary Proxmox host and additional compute/storage services |
| Storage     | Avid 18‑bay chassis populated with mixed SAS/SATA drives; EqualLogic‑backed storage       | Bulk storage and shared storage pools                        |
| Network     | Dell X1052P 52‑port switch; dual shielded Cat6 patch panels; OpenGear console manager;    | Core switching, structured cabling, and OOB serial access    |
|             | StarTech rack KVM and HP TFT5600 console                                                  | Local VGA/USB access for management                          |
| Security    | Cisco ASA 5510 / 5515‑X firewalls; SonicWall SRA 4200                                      | Perimeter firewalls and SSL VPN remote‑access gateway        |
| Monitoring  | Panasonic Toughbook CF‑30 running NST/SELKS with Suricata                                  | Log sink and IDS/IPS SOC dashboard                           |

### 2.2 Rack Philosophy

The rack is wired so that:

- All copper links pass through the patch panels into the core switch, keeping cabling predictable and serviceable.
- Management ports are aggregated on the console manager, with local VGA/USB access via the rack KVM and console.
- Power and data cabling are separated for easier maintenance and troubleshooting.

---

## 3. Logical Architecture

At a high level, the lab is split into distinct network zones, each mapped to its own VLAN and enforced by firewall policy.  
Inter‑VLAN routing is handled by the firewalls; the core switch provides Layer‑2 segmentation and mirroring for DPI.

### 3.1 Network Zones (Sanitized Overview)

| Zone        | Example VLAN ID | Role / Typical Hosts                           |
|------------|------------------|------------------------------------------------|
| Management | 10               | Switch, firewalls, console manager, iDRAC, SOC |
| Core       | 20               | Proxmox nodes, storage, shared services        |
| DMZ        | 30               | Public‑facing lab services                     |
| Lab        | 40               | General workloads, test VMs                    |
| Honeypots  | 50               | Intentionally exposed services                 |
| Guest      | 60               | Untrusted devices and Wi‑Fi clients           |

> **Note:** VLAN IDs and IP ranges above are examples only and do not reflect the exact addressing scheme in use.

### 3.2 Traffic Flow (Conceptual)

Typical flows include:

- **Internet ↔ ASA/SonicWall ↔ DMZ services** – For testing externally reachable services and VPN access.
- **Lab/Guest ↔ ASA ↔ Internet** – Outbound access is restricted and logged; selected traffic is mirrored to Suricata.
- **Honeypots ↔ ASA ↔ Internet** – Tight outbound controls with full monitoring of inbound scans and attacks.
- **Management ↔ All zones (controlled)** – Administrative access is limited to specific management endpoints and protocols.

An accompanying diagram in `diagrams/logical-network-diagram.png` illustrates how these zones connect through the firewall and core switch.

---

## 4. Security and Monitoring Design

### 4.1 Perimeter and Segmentation

- **Cisco ASA 5510 / 5515‑X** provide firewalling, NAT, and site‑to‑site/VPN functions.
- **SonicWall SRA 4200** terminates remote user VPN sessions.
- VLANs on the core switch implement basic separation of zones; ASA policies define which flows are permitted between them.
- Management interfaces are only reachable from the Management zone.

### 4.2 Deep Packet Inspection and Logging

- The Toughbook CF‑30 runs NST/SELKS with Suricata for deep packet inspection and alerting.
- Select traffic is mirrored from the core switch and firewall into Suricata, following the principle of inspecting important flows **once** rather than duplicating them.
- Log sources include firewalls (connection logs, VPN events), Proxmox and core services, honeypot and DMZ hosts, and network devices where useful.

Design considerations aim to balance coverage and efficiency: critical paths are inspected at well‑chosen points, and logs are centralized for correlation and investigation.

### 4.3 Honeypots and Exposure

A dedicated Honeypots zone exists for intentionally exposed services:

- Hosts in this zone can be selectively exposed through the ASA to the Internet.
- Outbound traffic from Honeypots is tightly controlled to prevent unintended pivoting.
- All Honeypot activity is logged and, where feasible, mirrored to Suricata for inspection.

The goal is to study scan and attack patterns in a controlled way, not to participate in abusive activity. The environment is designed to avoid unintended impact on networks outside the lab.

---

## 5. Operations and Procedures

Even though this repository omits live secrets and full device configurations, it reflects the operational structure used to keep the lab maintainable:

- **Configuration capture and backup** – Regular exports of sanitized device configurations and Proxmox backups are taken; secrets are stored offline.
- **Change logging** – Topology changes, new VLANs, firewall rule adjustments, and service deployments are noted in `runbooks/change-log.md` to keep design and implementation aligned.
- **Recovery drills** – Restoration of virtual machines, recreation of firewall rules from documentation, and verification that logging and Suricata restart cleanly after maintenance.

Detailed runbooks live in the `runbooks/` folder; they provide step‑by‑step procedures that can be followed by someone other than the original builder.

---

## 6. Repository Layout

The documentation and examples are organized as follows:

- `docs/` – Markdown documentation covering the overall narrative, hardware inventory, network and security architecture, service mapping, operations, and future roadmap.
- `diagrams/` – Visuals such as rack layouts, the logical network diagram, and other supplemental flowcharts.
- `infra/` – Sanitized technical examples, including example firewall policies, conceptual Ansible snippets, and utility scripts.
- `runbooks/` – Operational procedures such as backup/restore steps, incident response workflows, and change logs.
- `assets/photos/` – Redacted photos of the rack and environment, with identifying details avoided or blurred.

This structure makes it easy for a visitor to move from high‑level architecture down to specific examples without needing access to the physical rack.

---

## 7. Sanitization and Ethics

All IP addresses, hostnames, keys, credentials, and VPN details in this repository are **sanitized examples only**. Real secrets and identifying data are stored offline and are never committed to Git.

The lab is strictly for personal education and experimentation. It is isolated from production or customer systems. Any traffic analysis, IDS/IPS tuning, or honeypot activity is conducted within legal and ethical boundaries, and the environment is designed to avoid impacting networks outside the lab.

---