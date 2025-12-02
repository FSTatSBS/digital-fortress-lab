# Digital Infrastructure Lab

<div align="center">
  <img src="/assets/photos/test2.jpeg" alt="Enterprise Rack Configuration" width="75%" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
</div>

<div align="center" style="margin-top: 16px;">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat&logo=proxmox&logoColor=white" alt="Lab Status: Active"/>
  <img src="https://img.shields.io/badge/Built-Solo-1182c3?style=flat&logo=github&logoColor=white" alt="Built Solo"/>
  <img src="https://img.shields.io/badge/Documentation-Comprehensive-ff8800?style=flat&logo=markdown&logoColor=white" alt="Comprehensive Documentation"/>
  <img src="https://img.shields.io/badge/Nerd_Factor-11/10-ff0066?style=flat&logo=dependabot&logoColor=white" alt="Nerd Factor"/>
</div>

<details open>
<summary><strong>Introduction</strong></summary>

This repository details the architecture, implementation, and management of a dedicated digital infrastructure laboratory. Built on genuine enterprise hardware, it provides a secure, isolated environment for designing, testing, and refining network topologies, security measures, and operational frameworks.

</details>

> [!IMPORTANT]  
> Engineered with production-level standards on authentic hardware, accompanied by exhaustive documentation to support professional development and portfolio enhancement.

> [!NOTE]  
> Operated in complete isolation from production environments to enable risk-free experimentation with realistic scenarios.

## At a Glance — Current as of December 2025

<div align="center" style="margin-bottom: 20px;">
  <table style="width: 80%; border-collapse: collapse; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">
    <thead>
      <tr style="background-color: #f4f4f4;">
        <th style="padding: 10px; border: 1px solid #ddd; text-align: left;">Component</th>
        <th style="padding: 10px; border: 1px solid #ddd; text-align: left;">Specification</th>
        <th style="padding: 10px; border: 1px solid #ddd; text-align: left;">Status</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">Hypervisor</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Proxmox VE on Dell R710 (128 GB RAM, dual Xeon)</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Stable ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">Storage</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Dual EqualLogic FS7610 + Avid 18-bay chassis</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Redundant ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">Core Switch</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Dell X1052P — 52-port, full VLAN trunking</td>
        <td style="padding: 10px; border: 1px solid #ddd;">L2 Master ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">Perimeter</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Cisco ASA 5510/5515-X + SonicWall SRA 4200</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Hardened ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">SOC Node</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Panasonic Toughbook → NST/SELKS + Suricata</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Live DPI ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">Network Model</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Multi-zone, ASA-only L3 routing</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Zero Trust–inspired ✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #ddd;">OOB Management</td>
        <td style="padding: 10px; border: 1px solid #ddd;">OpenGear CM4148 + rack KVM + HP TFT5600</td>
        <td style="padding: 10px; border: 1px solid #ddd;">Always reachable ✅</td>
      </tr>
    </tbody>
  </table>
</div>

<div align="center" style="margin-top: 20px;">
  <strong>Lab Maturity</strong><br>
  <progress value="94" max="100" style="width: 50%; height: 20px;"></progress> <span style="font-weight: bold; font-size: 1.2em;">94%</span>
</div>

<details>
<summary><strong>Additional Notes</strong></summary>
<p>
This snapshot reflects the lab's configuration as of December 2025, emphasizing enterprise-grade components and operational stability. All systems are monitored for uptime and performance.
</p>
</details>


































































































## Table of Contents

<details open>
<summary><strong>Click sections to collapse/expand</strong></summary>

- [Purpose & Philosophy](#purpose--philosophy)
- [Physical Platform Gallery](#physical-platform-gallery)
- [Logical Architecture & Zones](#logical-architecture--zones)
- [Mermaid Traffic Flow Masterpiece](#mermaid-traffic-flow)
- [Security & Observability Stack](#security--observability)
- [Repository Structure](#repository-structure)
- [Professional Impact](#professional-impact)
- [Operations Discipline](#operations-discipline)
- [100% Solo Operator](#solo-operator)
- [Sanitization & Safety](#sanitization--safety)

</details>

## Purpose & Philosophy

This lab exists to **break things safely, document everything, and level-up**.

- Model real enterprise networks at 1/1000th the cost  
- Prototype firewall policies that survive red-team scrutiny  
- Feed honeypots to the internet and reverse-engineer attacks  
- Practice change management as if auditors were watching  
- Build observability that actually works  

~~A rack of old gear~~ → **A living, breathing portfolio masterpiece**

**Key Definitions**  
**Lab** :: Controlled environment for high-signal R&D  
**Operator** :: One human, infinite coffee  
**End State** :: Reproducible from this repo in <48 hours

## Physical Platform — Rack Porn Gallery

<details open>
<summary><strong>Compute & Storage</strong> — Click to collapse</summary>
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

## Logical Architecture & Zones

| Zone       | Trust     | Color | Purpose                              |
|------------|-----------|-------|--------------------------------------|
| Management | Highest   | Blue  | Crown jewels & consoles              |
| Core       | High      | Green | Proxmox + storage                    |
| DMZ        | Medium    | Yellow| Controlled exposure                  |
| Lab        | Medium    | Orange| General workloads                    |
| Honeypots  | Low       | Red   | Attack surface bait                  |
| Guest      | Lowest    | Black | Untrusted devices                    |

### Traffic Flow — Mermaid Masterpiece

```mermaid
graph TD
    subgraph "Internet"
        EXT[Internet<br>Scans • Bots • Script Kiddies] 
    end
    subgraph "Perimeter"
        ASA[ASA Outside<br>Cisco Firepower]
        SRA[SonicWall SRA<br>VPN Gateway]
    end
    subgraph "Trusted"
        MGMT[Management Zone]
        CORE[Core Zone]
        DMZ[DMZ Zone]
        LAB[Lab Zone]
        HONEY[Honeypots]
        GUEST[Guest Zone]
    end
    subgraph "Observability"
        SOC[SOC Node<br>Suricata + SELKS]
    end

    EXT -->|Controlled| ASA
    ASA --> DMZ & CORE & LAB & GUEST
    ASA --> SRA --> MGMT
    HONEY --> ASA
    SOC -.->|SPAN + Syslog| ASA & DMZ & HONEY

    classDef danger fill:#ff5555,stroke:#c00,color:white
    classDef secure fill:#55ff55,stroke:#080,color:black
    classDef neutral fill:#5555ff,stroke:#00c,color:white
    class EXT,HONEY danger
    class MGMT,CORE secure
    class DMZ,LAB,GUEST,SRA neutral
    class SOC fill:#ffff55,stroke:#aa0,color:black

## Repository Structure

```bash
digital-infrastructure-lab/
├── docs/                  # Architecture deep-dives & runbooks
├── diagrams/              # Mermaid + exported Visio diagrams
├── infra/                 # Sanitized ASA configs + Ansible samples
├── runbooks/              # Change log, procedures, rollback plans
└── assets/
    └── photos/            # The rack beauty you’re enjoying right now
Recommended starting point → docs/00_overview.md


### Block 9 – Professional Impact (Portfolio Gold)

```markdown
## Professional Impact — This Is Portfolio Gold

| Discipline                | Real-World Skills Demonstrated                                      |
|---------------------------|---------------------------------------------------------------------|
| Network Engineering       | Zone-based firewall design, ASA object-group mastery, VLAN architecture |
| Security Engineering      | Suricata IDS tuning, honeypot deployment, attack traffic analysis   |
| SRE / Platform Engineering| Full-stack observability, reproducibility, runbook discipline       |
| DevOps & Automation       | Ansible playbooks, config-as-code, documentation-as-code            |
| Technical Leadership      | End-to-end ownership, systems thinking, risk-aware design          |

> This single repository has replaced entire “homelab” sections on résumés.  
> Recruiters and senior engineers stop scrolling when they land here.

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




















