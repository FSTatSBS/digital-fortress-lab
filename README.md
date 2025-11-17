# Digital Fortress Lab

**Digital Fortress Lab** is my self-hosted security lab: a Proxmox-based virtualization stack on enterprise hardware, fronted by Cisco ASA and SonicWall firewalls, with VLAN segmentation, deep packet inspection, and a Suricata/SELKS SOC node.  

It is operated like a small production network, not a casual homelab.

---

## 1. Overview

This lab brings together compute, storage, networking, and security in a single, coherent environment where I can:

- Design and test security-focused architectures
- Practice change management, troubleshooting, and incident response
- Experiment with IDS/IPS, logging, and honeypots in a controlled setting
- Document infrastructure so it can be understood and maintained over time

---

## 2. Stack at a Glance

| Layer      | Components                                                                 |
|-----------|-----------------------------------------------------------------------------|
| Compute   | Dell PowerEdge R710, Dell EqualLogic FS7610 nodes running Proxmox          |
| Storage   | Avid 18-bay chassis with mixed SAS/SATA drives, EqualLogic-backed storage  |
| Network   | Dell X1052P core switch, dual Cat6 patch panels, OpenGear console manager, rackmount KVM |
| Security  | Cisco ASA 5510 / 5515-X, SonicWall SRA 4200 (VPN and remote access)        |
| Monitoring| Panasonic Toughbook CF-30 with NST/SELKS and Suricata (SOC/log sink)       |

Traffic is segmented into management, server, DMZ, honeypot, and guest networks, with movement between zones controlled by firewall policy and inspected where it makes sense.

---

## 3. What This Repo Demonstrates

This repository is not just an inventory of hardware. It is meant to show how I approach infrastructure and security in practice:

- **System thinking**  
  Network, compute, storage, and security are treated as one system with defined data flows and failure boundaries.

- **Segmentation and policy design**  
  VLANs and firewalls are used to create clear trust zones and to control how traffic moves between them.

- **DPI and logging placement**  
  Deep packet inspection and log collection are positioned so important traffic is inspected once, rather than bouncing through multiple tools.

- **Operational discipline**  
  Diagrams, notes, and runbooks capture how the environment is built, changed, and recovered, making it understandable to someone who has never seen the rack.

Over time this repository will accumulate:

- Rack and logical network diagrams
- Sanitized example firewall and VPN policies
- Notes on Proxmox, storage layout, and service placement
- Runbooks for backup/restore and incident response in the lab

---

## 4. How to Navigate This Repo

As content is added, the layout will evolve roughly as follows:

- **`docs/`** – Architecture, hardware inventory, VLAN layout, security design
- **`diagrams/`** – Rack front/rear views and logical network diagrams
- **`infra/`** – Sanitized examples of firewall rules, scripts, and infra-as-code concepts
- **`runbooks/`** – Backup/restore, incident response, and change log
- **`assets/photos/`** – Redacted photos of the rack and environment

For now, this README provides the high-level picture. Future updates will link directly to the most relevant documents inside `docs/`.

---

## 5. Sanitization and Ethics

All IP addresses, hostnames, keys, and credentials referenced in this repository are **sanitized examples only**. Real secrets and identifying details are never stored here.

The lab is strictly for personal education and experimentation. It is isolated from any production or customer systems, and all traffic analysis, IDS/IPS tuning, and honeypot activity is conducted within legal and ethical boundaries.
