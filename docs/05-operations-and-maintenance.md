# Operations and Maintenance

This document describes routine operational tasks for the Digital Fortress Lab. It acts as a high‑level reference to practices that keep the environment healthy, with detailed step‑by‑step instructions captured in individual runbooks.

## Backup Practices

- **Proxmox VM backups:** VMs are backed up on a regular schedule to external storage. Backups are rotated and integrity‑checked. Sensitive data within VM disks is encrypted at the guest OS level where appropriate.
- **Firewall and device configuration exports:** Sanitized configuration snapshots of ASA and SonicWall appliances, as well as switch config backups, are generated and stored offline. Secrets are never committed to the repository.
- **Runbook documentation:** After completing a backup, operators update the appropriate runbook or change log entry to record the date, scope, and any anomalies.

## Patch and Firmware Updates

- **Proxmox and guest OS updates:** Proxmox host packages and guest operating systems are kept current with upstream security updates. Non‑security package updates are applied in batches after testing.
- **Network and security appliances:** Firmware updates for the X1052P switch, ASA/SonicWall firewalls, and storage controllers are applied during scheduled maintenance windows. Release notes are reviewed for security fixes and regression risks.

## Hardware Checks and Monitoring

- **Environmental monitoring:** Rack temperature, airflow, and power consumption are monitored via onboard sensors and external tools where available. Alerts are configured to notify when thresholds are exceeded.
- **Disk health:** SMART data for all drives is periodically reviewed. Suspect drives are replaced proactively.
- **UPS testing:** Power backup systems (if present) are exercised to validate failover and runtime.

## Policy and Rule Review

- **Firewall rules:** On a regular cadence, firewall ACLs, NAT policies, and VPN configurations are reviewed to ensure they still align with the design intent. Redundant or outdated rules are removed and logged in the change log.
- **Logging and DPI:** Suricata signatures, alert thresholds, and log retention policies are tuned based on observed traffic patterns. False positives are reduced, and detection for relevant threats is refined.

## Runbooks

Detailed procedures for performing these tasks live in the `runbooks/` directory. Refer to those documents for step‑by‑step instructions, including commands to run, files to export, and validation steps.