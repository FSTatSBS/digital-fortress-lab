# Sample Ansible Playbooks

This directory is intended for conceptual examples of infrastructure‑as‑code approaches that could be applied to the Digital Fortress Lab.  
While the lab is primarily configured manually, automation concepts may be explored using tools like Ansible.

Potential playbook concepts:

- Deploy a new VLAN across the core switch and update the ASA policies accordingly (using sanitized host/port variables).
- Schedule configuration backups of ASA and SonicWall devices and store the results offline.
- Perform routine software updates on Proxmox and guest VMs in a controlled sequence.

All playbooks stored here should use placeholder addresses and credentials. Real secrets must be stored in vaults or excluded entirely.

---