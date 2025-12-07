# 04 ACL / Firewall Rules (Granular)

## Objective

Implement fine-grained firewall rules to control traffic between zones, enforce least-privilege access, and secure the lab environment. Document ACLs and integrate them with NAT and segmentation policies.

---

## 1. ASA ACL Configuration Examples

### Inside to Outside (Internet Access)

```bash
access-list inside_access extended permit ip any any
access-group inside_access in interface inside
```

### Inside to DMZ

```bash
access-list inside_dmz extended permit ip any 192.168.2.0 255.255.255.0
access-group inside_dmz in interface inside
```

### DMZ to Outside (HTTP/HTTPS Only)

```bash
access-list dmz_access extended permit tcp any any eq 80
access-list dmz_access extended permit tcp any any eq 443
access-group dmz_access in interface dmz
```

### VPN to Internal

```bash
access-list vpn_access extended permit ip 192.168.3.0 255.255.255.0 any
access-group vpn_access in interface vpn
```

### Management Access

```bash
access-list management_access extended permit ip 192.168.4.0 255.255.255.0 any
access-group management_access in interface management
```

---

## 2. SonicWall ACL / Access Rule Examples

```bash
access-rule add name "Inside-to-DMZ" from X1 to X2 action allow service any
access-rule add name "Inside-to-Outside" from X1 to X0 action allow service any
access-rule add name "VPN-to-Internal" from X3 to X1 action allow service any
access-rule add name "VPN-to-DMZ" from X3 to X2 action allow service any
access-rule add name "Management-to-All" from X4 to any action allow service any
```

---

## 3. Best Practices

* Apply principle of least privilege: only allow necessary protocols and subnets.
* Use **object groups** for networks, services, and users to simplify rule management.
* Document each ACL rule with purpose, owner, and last review date.
* Use **time-based ACLs** if temporary access is required.
* Ensure ACLs are **applied to correct interfaces** with proper direction (inbound/outbound).
* Test ACLs in a lab environment before production deployment.
* Monitor ACL logs for denied traffic and anomalies.
* Align ACLs with NAT and segmentation policies to prevent conflicts.
* Regularly review ACLs as part of change control and auditing.
* Consider context-aware or identity-based rules if supported by the firewall.

---

## 4. Advanced Recommendations

* Combine ACLs with QoS policies to prioritize critical lab traffic.
* Integrate firewall rules with SIEM for automated alerting.
* Maintain versioned ACL templates to standardize lab and production setups.
* Simulate attack scenarios to validate ACL effectiveness.
* Regularly reconcile ASA and SonicWall rules for consistency across devices.

---

## References

* Cisco ASA 5510/5515-X Configuration Guides
* SonicWall NSa Series Firewall Configuration Guide
* NIST Cybersecurity Framework – Acces
