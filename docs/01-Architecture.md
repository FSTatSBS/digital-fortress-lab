# 01 – Architecture

## Overview

EvoSec is a comprehensive lab environment for cybersecurity research and operational analysis. It supports multi-VM experiments, containerized services, and hypervisor snapshots — enabling flexible, reproducible, realistic testing environments.  

The platform integrates honeypots, tar pits, IDS/IPS systems, and provides dynamic network orchestration (VLAN reconfiguration), automated failure containment, and threat simulation.  

```mermaid
graph LR
    Lab["EvoSec-Lab Environment"] --> VM["Multi-VM Experiments"]
    Lab --> CT["Containerized Services"]
    Lab --> HS["Hypervisor Snapshots"]
    VM --> Flex["Flexible Testing"]
    CT --> Flex
    HS --> Flex
    Flex --> Res["Reproducible Results"]
