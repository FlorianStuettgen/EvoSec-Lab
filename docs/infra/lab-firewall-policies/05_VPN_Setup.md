# 05 VPN Setup (Site-to-Site & Remote Access)

## Objective

Configure secure VPN connectivity for remote users and site-to-site connections, ensuring encryption, authentication, and controlled access to lab networks.

---

## 1. ASA VPN Configuration

### IKEv1 Site-to-Site VPN

```bash
crypto ikev1 enable outside
crypto ikev1 policy 10
 authentication pre-share
 encryption aes
 hash sha
 group 2
 lifetime 86400
crypto ipsec ikev1 transform-set LAB-TRANSFORM esp-aes esp-sha-hmac
crypto map VPN-MAP 10 ipsec-isakmp
 set peer <PEER_IP>
 set transform-set LAB-TRANSFORM
 match address vpn_access
interface outside
 crypto map VPN-MAP
```

### Remote Access VPN (SSL VPN)

```bash
webvpn
 enable outside
 anyconnect image disk0:/anyconnect.pkg 1
 tunnel-group LAB-RA-VPN type remote-access
 tunnel-group LAB-RA-VPN general-attributes
 address-pool VPN_POOL
 authentication-server-group LOCAL
 default-group-policy LAB-RA-Policy
```

**Best Practices:**

* Use strong encryption (AES-256, SHA2) and DH groups.
* Implement split tunneling for lab networks to reduce exposure.
* Rotate pre-shared keys and certificates regularly.
* Limit VPN access by role, IP, and time.
* Enable logging and monitoring of VPN sessions.
* Test VPN connectivity for each critical subnet and service.

---

## 2. SonicWall VPN Configuration

### IKEv2 Site-to-Site VPN

```bash
vpn add name LAB-VPN policy ikev2 remote <PEER_IP> preshared-key <KEY> local-ip 192.168.3.1 remote-subnet 192.168.1.0/24,192.168.2.0/24
```

### Remote Access VPN

```bash
vpn add name LAB-RA-VPN policy ikev2 local-ip 192.168.3.1 preshared-key <KEY> user-group VPN_Users address-pool VPN_POOL
```

**Best Practices:**

* Use strong IKEv2 encryption and authentication.
* Separate remote access VPN users into dedicated groups.
* Enable two-factor authentication if supported.
* Limit access to necessary resources using VPN access rules.
* Monitor VPN activity and integrate with SIEM for alerts.
* Test failover and redundancy for critical VPN connections.

---

## 3. VPN Monitoring and Logging

* Enable detailed logging of tunnel establishment and termination.
* Track VPN user activity and source IP addresses.
* Alert on multiple failed login attempts or unusual connection patterns.
* Retain logs for compliance and auditing purposes.
* Use monitoring dashboards for session counts and bandwidth usage.

---

## 4. Advanced Recommendations

* Implement certificate-based authentication for site-to-site VPNs.
* Use segmented VPN pools for lab, dev, and management networks.
* Consider integrating VPN authentication with directory services (LDAP/AD).
* Apply granular ACLs to VPN traffic for each zone.
* Periodically audit VPN policies and remove unused tunnels.
* Simulate VPN failures to validate resilience and automatic reconnection.

---

## References

* Cisco ASA VPN Configuration Guides
* SonicWall NSa VPN Configuration Guides
* NIST SP 800-77 – Guide to IPsec VPNs
* CIS VPN Benchmarks for
