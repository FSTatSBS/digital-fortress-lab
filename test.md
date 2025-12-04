<h1 align="left"><strong>EvoSec-Lab</strong></h1>
<div align="left">
  <img src="/assets/photos/test2.jpeg" alt="Enterprise Rack Configuration" width="90%" style="border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);"/>
</div>
<div align="left" style="margin-top: 16px;">
  <img src="https://img.shields.io/badge/Status:-Active-brightgreen?style=for-the-badge&logo=proxmox&logoColor=white" alt="Lab Status: Active"/>
  <img src="https://img.shields.io/badge/Built:-Solo-blue?style=for-the-badge&logo=github&logoColor=white" alt="Build finished"/>
  <img src="https://img.shields.io/badge/Nerd_Factor:-11/10-pink?style=for-the-badge&logo=dependabot&logoColor=white" alt="Nerd Factor"/>
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge&logo=github&logoColor=white" alt="MIT License"/>
  <img src="https://img.shields.io/badge/LinkedIn-Florian_Stuettgen-blue?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn Profile"/>
</div>

> [!NOTE]  
>Engineered with production-level standards and documentation on authentic enterprise-grade hardware.  

> [!IMPORTANT]  
>Data sanitized. Sensitive information, credentials, or real network details are **obfuscated or excluded**.

---

<h2 align="left"><strong>What is this?</strong></h2>
<div align="left">

**EvoSec** is an isolated design and testing orchestration stage for Network Topologies, Security Measures & **Project Controls Workflows**.  

Enterprise-grade hardware, **Complex** network topologies, & Robust workflows integrated seamlessly.  

This lab serves as a hands-on playground for experimentation, learning, and proof-of-concept development, combining hardware, software, and automation in realistic, production-like scenarios.

---

<h3 align="left"><strong>Key Highlights:</strong></h3>

- **Enterprise-Grade Simulation**  
  Realistic network environments featuring racks, switches, and firewalls designed to mirror production-grade infrastructures.

- **Project Controls Workflows**  
  Structured processes for planning, monitoring, and managing complex IT and network operations.

- **Security Experimentation**  
  Controlled deployment of honeypots, tar pits, and monitoring systems for safe and practical security research.

- **Automation & Orchestration**  
  Integration of LLM and SaltStack to dynamically manage infrastructure and maintain operational consistency.

- **Isolated Testing Environment**  
  A fully contained lab that enables risk-free experimentation without any impact on live systems.

- **Thorough Documentation**  
  Detailed notes, diagrams, and procedures ensuring all setups are transparent, reproducible, and verifiable.


## At a Glance as of December 2025

<details open>
<summary><em style="color:#555; font-size:0.9em;">Overview of lab components, including specifications, roles, and operational status for a snapshot.</em></summary>

| Component       | Specification                            | Description                                                                 | Status |
|-----------------|-----------------------------------------|----------------------------------------------------------------------------|--------|
| Hypervisor      | Proxmox VE on Dell R710 (128 GB RAM, dual Xeon) | Foundational virtualization platform enabling efficient VM and container management with high resource utilization and failover capabilities. | **Operational and Stable** |
| Storage         | Dual EqualLogic FS7610 + Avid 18-bay chassis | Scalable, high-performance NAS storage with RAID redundancy, supporting iSCSI and NFS. | **Fully Redundant** |
| Core Switch     | Dell X1052P — 52-port, full VLAN trunking | Central Layer 2 switch handling VLAN segmentation, PoE, and high-throughput traffic. | **L2 Master Operational** |
| Perimeter       | Cisco ASA 5510/5515-X + SonicWall SRA 4200 | Security boundary with adaptive firewalling, VPN support, and intrusion prevention. | **Hardened and Secure** |
| SOC Node        | Panasonic Toughbook → NST/SELKS + Suricata | Security operations center node for real-time monitoring, ELK integration, IDS/IPS. | **Live DPI Active** |
| Network Model   | Multi-zone, ASA-only L3 routing          | Segmented, zero-trust architecture with Layer 3 routing confined to ASA devices. | **Zero Trust Enforced** |
| OOB Management  | OpenGear CM4148 + rack KVM + HP TFT5600 | Out-of-band management console for remote access and KVM-over-IP. | **Always Accessible** |

</details>

## Physical Platform

<details>
<summary><strong>Compute & Storage</strong></summary>

<br>
<img src="/assets/photos/Compute1.jpg" alt="R710" loading="lazy" width="100%"/>
<img src="/assets/photos/Compute2.png" alt="EqualLogic" loading="lazy" width="100%"/>
<img src="/assets/photos/Storage1.png" alt="Avid" loading="lazy" width="100%"/>

</details>

<details>
<summary><strong>Network & OOB Management</strong></summary>

<br>
<img src="/assets/photos/switch.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/patch.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/console3.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/console1.jpg" loading="lazy" width="100%"/>

</details>

<details>
<summary><strong>Security & SOC Node</strong></summary>

<br>
<img src="/assets/photos/sec1.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/sec3.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/sec2.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/monitor1.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/monitor2.jpg" loading="lazy" width="100%"/>

</details>


<h3 align="left"><strong>With full operational maturity, the lab now operates as a dynamic, self-regulating security environment.</strong></h2>

The interplay here is complex, but charted here is a naive approach:

<div align="left">
  <img src="https://github.com/FlorianStuettgen/digital-infrastructure-lab/blob/main/assets/photos/diagram.svg" alt="System Diagram" width="1000"/>
  <p><i>
  System architecture showing compute, storage, and network topology. Application VMs run critical services on isolated VLANs, while honeypots and tar pits detect and slow threats. 
  SaltStack orchestrates real-time network adjustments, moving VMs and activating traps as needed. 
  LLM-driven analytics are reacting to the logs, anticipating attacks, and dynamically adjusting the network topology.</i></p>
</div>

## Logical Architecture & Zones

| Zone       | Trust     | Color | Purpose                              |
|------------|-----------|-------|--------------------------------------|
| Management | Highest   | Blue  | Crown jewels & consoles              |
| Core       | High      | Green | Proxmox + storage                    |
| DMZ        | Medium    | Yellow| Controlled exposure                  |
| Lab        | Medium    | Orange| General workloads                    |
| Honeypots  | Low       | Red   | Attack surface bait                  |
| Guest      | Lowest    | Black | Untrusted devices                    |

### Block 9 – Professional Impact 

| Discipline                | Real-World Skills Demonstrated                                      |
|---------------------------|---------------------------------------------------------------------|
| Network Engineering       | Zone-based firewall design, ASA object-group mastery, VLAN architecture |
| Security Engineering      | Suricata IDS tuning, honeypot deployment, attack traffic analysis   |
| SRE / Platform Engineering| Full-stack observability, reproducibility, runbook discipline       |
| DevOps & Automation       | Ansible playbooks, config-as-code, documentation-as-code            |
| Technical Leadership      | End-to-end ownership, systems thinking, risk-aware design          |

## 100% Solo Operator

Every cable pulled, every ACL written, every diagram drawn, every line of Markdown — **one human**.

- Sourced and refurbished all enterprise hardware  
- Designed every security zone and policy from scratch  
- Stood up Proxmox, ASA, SonicWall, Suricata, SELKS  
- Authored the entire documentation suite and runbooks  
- Still adding features at 2 a.m. because it’s fun

<p align="center">
  <strong>Built with precision.<br>Documented with obsession.<br>Operated with fire.</strong>
  <br><br>
  <img src="https://img.shields.io/badge/Level-Over_9000-ff0066?style=for-the-badge&logo=dependabot" alt="Over 9000"/>
  <br><br>
  <a href="#digital-infrastructure-lab">Back to Top</a>
</p>
