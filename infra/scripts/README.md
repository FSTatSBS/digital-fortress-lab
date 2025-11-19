# Infra Scripts

This directory is reserved for helper scripts used to manage the Digital Fortress Lab.  
Scripts included here are examples and conceptual placeholders; they are not meant to be run as‑is without adjustment and proper secrets management.

Examples of potential scripts include:

- Backup automation for firewall configurations and Proxmox VMs (with sensitive details stored offline).
- Health‑check routines that query device status, disk health, and log file sizes.
- Helper functions to parse and archive logs from Suricata or syslog sources.

When adding scripts to this directory, ensure that:

1. No secrets, passwords, or keys are embedded in the files.
2. The scripts are clearly documented with usage instructions and prerequisites.
3. They are committed only when sanitized and safe to share.

---