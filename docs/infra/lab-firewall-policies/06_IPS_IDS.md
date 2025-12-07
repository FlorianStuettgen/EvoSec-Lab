# 06 IPS/IDS & Advanced Threat Protection

## Objective

Enable and configure Intrusion Prevention Systems (IPS) and Intrusion Detection Systems (IDS) to monitor, detect, and mitigate threats across the lab network, including external, DMZ, and internal zones. Integrate advanced threat protection mechanisms for proactive security.

---

## 1. ASA IPS/IDS Configuration

### Basic Threat Detection

```bash
threat-detection basic-threat
threat-detection statistics
```

### URL Filtering and Advanced Threat (if licensed)

```bash
! Enable URL filtering and botnet traffic detection
```

**Best Practices:**

* Enable IPS/IDS on external and DMZ interfaces.
* Regularly update threat signatures and pattern files.
* Monitor alert logs and integrate with SIEM for real-time detection.
* Conduct periodic tuning of IPS/IDS rules to reduce false positives.
* Document enabled IPS/IDS features per interface and zone.
* Use logging thresholds to avoid overwhelming the management plane.

---

## 2. SonicWall IPS/IDS Configuration

```bash
set security-services enable
set ips enable
set gateway-anti-virus enable
set gateway-anti-spyware enable
```

**Best Practices:**

* Apply IPS policies to all external-facing interfaces and sensitive internal zones.
* Enable gateway antivirus and anti-spyware for DMZ and lab/dev zones.
* Integrate alerts with SIEM or central logging servers.
* Schedule automatic updates for IPS signatures and threat intelligence feeds.
* Monitor for anomalous traffic patterns indicative of advanced threats.
* Enable deep packet inspection where available for critical traffic.

---

## 3. Advanced Threat Protection

* Implement sandboxing or behavioral analysis for suspicious files.
* Use threat intelligence feeds to enhance detection capabilities.
* Segment network for critical lab systems to prevent lateral movement.
* Combine IPS/IDS with ACLs and NAT rules for multi-layered defense.
* Periodically conduct penetration tests to validate effectiveness.
* Document response procedures for detected threats.
* Integrate alerts with automated response systems where possible.

---

## 4. Logging and Monitoring

* Centralize IPS/IDS logs to SIEM for correlation.
* Configure alerts for critical events and threshold violations.
* Maintain historical data for trend analysis and incident investigation.
* Periodically review and fine-tune rules based on detected incidents.
* Ensure all logs include device hostname and interface for context.

---

## References

* Cisco ASA 5510/5515-X IPS/IDS Guides
* SonicWall NSa Series Security Services Configuration Guide
* NIST SP 800-94 – Guide to Intrusion Detection and Prevention Systems
* CIS Benchmarks – Firewall and IPS/IDS Best Practices
