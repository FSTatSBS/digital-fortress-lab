# Future Roadmap

This document tracks planned improvements and experiments for the Digital Fortress Lab. It serves as a living backlog of ideas rather than a commitment to specific timelines. Items may be added, removed, or reprioritized as the environment evolves.

## Planned Enhancements

- **Expand network diagrams and service maps:** Create detailed topology diagrams for each zone, including host names, service ports, and data flows.
- **Document service deployment:** Write installation and configuration guides for core services (directory, DNS, NTP, log aggregation) and link them from the services document.
- **Refine firewall policy examples:** Add more examples of ASA and SonicWall configurations, including VPN setups, IPSec tunnels, and SSL VPN profiles.
- **Automate backups and checks:** Introduce scripts or Ansible playbooks to automate configuration backups, VM snapshots, and health checks. Track these in `infra/` with placeholders for secrets.
- **Experiment with new hardware:** Integrate additional networking or security devices (e.g., newer firewalls, IDS sensors) and document the design changes.
- **Integrate with external labs:** Connect the lab to external environments via VPN or routed links to test site‑to‑site scenarios and multi‑lab experiments.

## Short‑Term Goals

- Finalize the hardware inventory and ensure the documentation matches the actual rack.
- Draw a detailed rack layout diagram (front and rear) for the `diagrams/` directory.
- Populate the services document with current VMs, including hostnames, IPs (sanitized), and installed roles.

## Long‑Term Goals

- Build out a small PKI to issue certificates for internal services and VPNs.
- Explore container orchestration (e.g., Kubernetes) within the lab and document how it integrates with existing infrastructure.
- Set up continuous integration pipelines for infrastructure as code (testing Ansible playbooks, configuration templating, etc.).

---

This roadmap will be updated as the environment grows. Contributions, suggestions, and critiques are welcome to help improve the design and documentation.