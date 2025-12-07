# 01_Hostname, Domain, and Management Access

## Objective

Secure administrative access, enforce role-based authentication, enable audit logging, and monitor management activity across the lab environment. This section ensures a secure management plane and establishes the foundation for all lab operations.

---

## 1. Hostname and Domain Configuration

**Purpose:** Ensure devices are uniquely identifiable and integrated into lab DNS and domain policies.

### ASA Example:

```bash
hostname LAB-FW
domain-name lab.local
```

### SonicWall Example:

```bash
configure
set hostname LAB-FW
```

**Best Practices:**

* Use descriptive hostnames indicating device type, role, and location.
* Ensure domain-name matches internal DNS lab domain.
* Document hostname and domain mapping in lab inventory.

---

## 2. Administrative Access Configuration

**Purpose:** Limit and secure access to only authorized personnel.

### ASA Example:

```bash
enable password <ENCRYPTED_PASSWORD> privilege 15
ssh 192.168.1.0 255.255.255.0 inside
ssh version 2
ssh timeout 120
aaa authentication ssh console LOCAL
http 192.168.1.0 255.255.255.0 inside
```

### SonicWall Example:

```bash
set admin-password <STRONG_PASSWORD>
set admin-management enable https ssh
set admin-management-interface X4
```

**Best Practices:**

* Enforce **MFA** for all management sessions.
* Limit admin access to dedicated **management VLAN**.
* Restrict SSH and HTTPS to specific source IPs.
* Use **role-based access control (RBAC)** to separate roles (monitoring, admin, auditor).
* Configure session timeouts and login lockouts to prevent brute-force attacks.
* Maintain a secure **password rotation schedule** and store credentials encrypted.
* Enable **AAA logging** to track all login attempts.
* Audit user accounts periodically for compliance.

---

## 3. SNMP and Monitoring Access

**Purpose:** Enable monitoring and alerting without compromising security.

### ASA Example:

```bash
snmp-server enable traps snmp
snmp-server host inside 192.168.1.20 community <COMMUNITY_STRING>
```

### SonicWall Example:

```bash
set snmp enable
set snmp-community <COMMUNITY_STRING>
set snmp-traps enable
```

**Best Practices:**

* Use SNMPv3 if supported for secure authentication and encryption.
* Limit SNMP access to monitoring servers only.
* Integrate SNMP traps with SIEM for real-time alerts.
* Document SNMP community strings and usage.
* Rotate SNMP credentials regularly.

---

## 4. Logging Configuration

**Purpose:** Maintain audit trails for administrative actions, troubleshooting, and compliance.

### ASA Example:

```bash
logging enable
logging buffered informational
logging trap informational
logging host inside 192.168.1.10
logging host inside 192.168.1.15 transport udp port 514
```

### SonicWall Example:

```bash
set logging enable
logging set level informational
logging host 192.168.1.10
set syslog enable
set syslog-host 192.168.1.15 port 514
```

**Best Practices:**

* Centralize logs to a **SIEM** or log server.
* Define logging levels per interface and service.
* Enable **alerts for critical events** (login failures, ACL violations, configuration changes).
* Maintain **retention policies** for audit and compliance.
* Include device hostname in logs for correlation.
* Regularly review logs for anomalies or misconfigurations.

---

## 5. Security Hardening and Additional Recommendations

* Disable unused services (e.g., Telnet, FTP, HTTP if HTTPS is used).
* Enforce strong ciphers for SSH and HTTPS; disable TLS <1.2.
* Configure **login banners** specifying monitoring and authorization notices.
* Backup configuration files securely and regularly.
* Implement **change control** for administrative account modifications.
* Conduct **periodic access reviews** and log audits.
* Use **temporary accounts** for lab experiments and remove after use.
* Integrate configuration monitoring for **unauthorized changes**.

---

## Notes

This section focuses on **management plane security**, laying the foundation for secure lab operations. Proper configuration ensures all subsequent policies (ACLs, segmentation, VPNs, NAT) are applied and monitored safely. Compliance, auditing, and operational transparency are key objectives.

---

## References

* Cisco ASA 5510/5515-X Configuration Guides
* SonicWall NSa Series Security Configuration Guides
* NIST Cybersecurity Framework
* CIS Security Benchmarks for Firewalls
