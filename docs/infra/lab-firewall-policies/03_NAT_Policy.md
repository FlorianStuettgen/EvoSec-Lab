# 03 NAT Policy (Dynamic & Static)

## Objective

Configure Network Address Translation (NAT) for lab networks to ensure secure internet access, DMZ exposure, and VPN connectivity. Implement NAT exemptions where needed and maintain detailed auditing of NAT rules.

---

## 1. ASA NAT Configuration

### Dynamic NAT (Internet Access)

```bash
object network obj_any
 subnet 0.0.0.0 0.0.0.0
 nat (inside,outside) dynamic interface

object network obj_dmz
 subnet 192.168.2.0 255.255.255.0
 nat (dmz,outside) dynamic interface

object network obj_vpn
 subnet 192.168.3.0 255.255.255.0
 nat (vpn,outside) dynamic interface

object network obj_lab
 subnet 192.168.5.0 255.255.255.0
 nat (lab,outside) dynamic interface
```

### NAT Exemption (VPN / Management)

```bash
nat (inside,vpn) 0 access-list inside_vpn_no_nat
access-list inside_vpn_no_nat extended permit ip 192.168.1.0 255.255.255.0 192.168.3.0 255.255.255.0
```

### Static NAT (DMZ Servers)

```bash
object network obj_websrv
 host 192.168.2.10
 nat (dmz,outside) static 203.0.113.10
```

**Best Practices:**

* Combine dynamic NAT for internet access with static NAT for DMZ/public-facing services.
* Exclude VPN and management subnets from NAT to maintain end-to-end connectivity.
* Regularly review NAT rules and remove unused or redundant entries.
* Maintain documentation of NAT mappings and intended use cases.
* Test NAT behavior after firewall or interface changes.

---

## 2. SonicWall NAT Configuration

### Dynamic NAT Example

```bash
nat-policy add from X1 to X0 src any dst any service any
nat-policy add from X2 to X0 src any dst any service any
nat-policy add from X3 to X0 src any dst any service any
nat-policy add from X5 to X0 src any dst any service any
```

### NAT Exemption (VPN)

```bash
nat-policy add from X1 to X3 src 192.168.1.0/24 dst 192.168.3.0/24 service any no-nat
```

### Static NAT for DMZ

```bash
nat-policy add from X2 to X0 src 192.168.2.10 dst 203.0.113.10 service any
```

**Best Practices:**

* Maintain consistency in NAT policies across all firewalls.
* Document static NAT mappings for audit and troubleshooting.
* Limit exposure of DMZ hosts with static NAT; only allow required services.
* Use object groups to simplify NAT configuration and reduce human error.
* Monitor NAT translations and session counts for anomalies.

---

## 3. Logging and Monitoring NAT

**Purpose:** Ensure transparency and track unusual activity.

**Best Practices:**

* Enable NAT logging to a central SIEM.
* Include object names and interface references in logs.
* Alert on NAT failures or unexpected translations.
* Periodically reconcile NAT rules against the lab network topology.
* Include NAT configuration in change-control procedures.

---

## 4. Advanced Recommendations

* Implement NAT for lab experiments in isolated zones to prevent accidental exposure.
* Use separate NAT pools for high-risk or public-facing services.
* Combine NAT with ACLs to enforce fine-grained security policies.
* Document intended traffic flows for each NAT rule.
* Automate NAT auditing with scripts or configuration management tools.

---

## References

* Cisco ASA 5510/5515-X NAT Configuration Guides
* SonicWall NSa NAT Policy Configuration Guide
* NIST Cybersecurity Framework – Network Traffic Segment
