# 04 – Network Topology

EvoSec uses a multi-zone, segmented network topology to isolate different parts of the lab and control traffic flow.  

## Zones / VLANs

- **Management Network** — administrative access, orchestration, provisioning  
- **Honeypot Zone** — isolates and logs attacker activity  
- **DMZ / Public-facing Zone** — services exposed to external networks  
- **Internal / Research Zone** — sandbox environment for research VMs/containers  
- **Isolation / Containment Zone** — quarantines suspicious VMs/traffic

## Network Controls & Flow

- VLAN-based segmentation strictly separates zones  
- Dynamic VLAN reconfiguration allows rapid isolation  
- Traffic filtering, proxying, tar-pit slowing, and containment  
- Logging and monitoring on all inter-zone traffic
