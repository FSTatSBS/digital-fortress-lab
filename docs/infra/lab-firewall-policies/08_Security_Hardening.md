# 08 Security Hardening & Best Practices

## Objective

Implement security hardening measures on ASA and SonicWall firewalls to reduce attack surface, enforce best practices, and maintain a secure lab environment.

---

## 1. Service & Interface Hardening

* Disable unused services and interfaces.
* Enforce SSH/HTTPS management only; disable Telnet and HTTP.
* Use dedicated management VLAN for administrative access.
* Apply IP verification and anti-spoofing measures.
* Limit SNMP access to trusted monitoring systems only.
* Use strong passwords and encrypted credentials.

### ASA Example

```bash
no ip http server
no ip http secure-server
ssh timeout 120
aaa authentication ssh console LOCAL
username admin password <STRONG_PASSWORD> privilege 15
```

### SonicWall Example

```bash
set admin-management enable https ssh
set admin-management-interface X4
set admin-password <STRONG_PASSWORD>
```

---

## 2. ACL & Object Group Hardening

* Apply principle of least privilege on ACLs.
* Use object groups for networks, services, and users.
* Regularly review and remove obsolete rules.
* Document ACL rules with purpose, owner, and last review date.
* Implement time-based ACLs for temporary access.

---

## 3. VPN & Authentication Security

* Use strong encryption (AES-256, SHA2) and secure DH groups.
* Implement certificate-based authentication where possible.
* Enable two-factor authentication for remote access VPN.
* Regularly rotate pre-shared keys and certificates.
* Segment VPN access by roles and project networks.

---

## 4. IPS/IDS & Advanced Threat Protection

* Enable IPS/IDS on all external and sensitive internal interfaces.
* Update threat signatures and patterns regularly.
* Enable gateway anti-virus, anti-spyware, and web filtering.
* Conduct periodic tuning to reduce false positives.
* Document IPS/IDS configuration and alerts.

---

## 5. Logging & Monitoring Security

* Centralize logs to SIEM or syslog servers.
* Enable logging for configuration changes, authentication events, and security incidents.
* Monitor for anomalies in management access and interface traffic.
* Retain logs according to compliance and operational requirements.
* Integrate monitoring alerts into operational workflows.

---

## 6. System Updates & Patch Management

* Apply firmware and patch updates regularly.
* Test updates in lab environment before production deployment.
* Maintain version control and change logs.
* Subscribe to vendor security advisories for proactive response.

---

## 7. Backup & Recovery

* Regularly backup configuration files and store securely.
* Validate backup integrity periodically.
* Document recovery procedures for quick restoration.
* Maintain snapshots of critical configurations.

---

## 8. Lab Segmentation & Testing

* Conduct experiments in isolated lab environments.
* Limit lab traffic exposure to production networks.
* Document all testing scenarios, network changes, and results.
* Implement rollback procedures for experimental configurations.

---

## 9. Documentation & Compliance

* Maintain a versioned repository of firewall policies, ACLs, NAT, VPN, and monitoring configurations.
* Document all security hardening measures, rationale, and responsible owners.
* Schedule periodic security audits.
* Align lab practices with NIST, CIS, and internal compliance frameworks.

---

## References

* Cisco ASA 5510/5515-X Security Hardening Guides
* SonicWall NSa Series Hardening & Best Practices Guide
* NIST SP 800-53 – Security and Privacy Controls
* CIS Firewall Benchmarks for ASA and SonicWall
