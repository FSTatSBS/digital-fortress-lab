# Security Architecture

This document describes how security is structured in the Digital Fortress Lab: perimeter controls, segmentation, monitoring, and how the different components fit together. Details are intentionally high‑level and sanitized; the focus is on design rather than raw configuration.

---

## Security Objectives

The lab is built to:

- Isolate experiments from household and external networks.
- Practice designing firewall and VPN policy on real appliances.
- Observe and analyze traffic with IDS/IPS and centralized logging.
- Test honeypot and exposure scenarios in a controlled way.

---

## Perimeter and Segmentation

### Perimeter Devices

- **Cisco ASA 5510 / 5515‑X** provide firewalling, NAT, and site‑to‑site/VPN capabilities.
- **SonicWall SRA 4200** provides SSL VPN and remote access for administrative connections into the lab.

The ASA and SonicWall sit between the lab and the outside world. Inbound and outbound flows pass through these devices, which enforce policy and provide logging.

### Network Zones

Security is built on the same zones described in the network architecture. VLANs implement logical separation on the switch; ASA policies govern which flows can cross between zones and which can reach the Internet.

---

## Management Access

Management interfaces are intentionally constrained:

- Administrative access to firewalls, switch, storage, and Proxmox is only allowed from the **Management** zone.
- Serial console access is centralized on the **OpenGear console manager**, with physical access controlled at the rack.
- The rack KVM and TFT5600 console provide local access only; no GUI management ports are exposed directly to the public Internet.

Authentication methods, exact addresses, and credentials are tracked privately and are not stored in this repository.

---

## Logging, Monitoring, and DPI

The Panasonic Toughbook CF‑30 functions as a small SOC node:

- Runs NST/SELKS with Suricata for deep packet inspection and alerting.
- Ingests firewall logs (connections, VPN events, system messages) and logs from Proxmox and core services.
- Receives mirrored traffic from selected switch ports and/or firewall interfaces.

Design considerations:

- Important flows are mirrored and inspected at a **small number of well‑chosen points** rather than duplicated across multiple tools.
- IDS/IPS signatures and alert thresholds can be tuned using traffic from the Honeypot and Lab zones without affecting production systems.

---

## Honeypots and Exposure

A dedicated **Honeypots** zone exists for intentionally exposed services:

- Hosts in this zone can be selectively exposed through the ASA to the Internet.
- Outbound traffic from Honeypots is tightly controlled to prevent unintended pivoting.
- All Honeypot activity is logged and, where feasible, mirrored to Suricata for inspection.

The purpose is to study scan and attack patterns, not to participate in abusive activity. The environment is designed to avoid unintended impact on networks outside the lab.

---

## Configuration Management and Recovery

Security‑relevant configuration is handled with the following discipline:

- Baseline firewall policies and key ASA/SonicWall concepts are documented in sanitized form in `infra/example-firewall-policies/`.
- Regular backups of firewall and Proxmox configurations are taken and stored **offline**; copies are not committed to this repository.
- When changes are made to rules, VPNs, or exposure of services, a short note is added to `runbooks/change-log.md` to keep design and implementation aligned.

The intention is that the entire security posture can be reconstructed from documentation and backups even if individual devices need to be replaced or re‑imaged.

---

## Example Policy Fragment

A sanitized ASA base policy fragment is included in:

* `infra/example-firewall-policies/asa-lab-base-policy.txt`

It shows the general structure of interface roles, network objects, NAT, and ACLs used to implement the zone model described in this document, without exposing real addresses or credentials.