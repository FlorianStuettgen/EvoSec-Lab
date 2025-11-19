# Digital Fortress Lab

Digital Fortress Lab is my self-hosted security environment, built on enterprise hardware and operated deliberately like a small production network rather than a casual homelab. It brings together Proxmox virtualization, Dell storage, Cisco ASA and SonicWall firewalls, VLAN-based segmentation, deep packet inspection, and a Suricata/SELKS SOC node into a single, coherent platform for infrastructure and security engineering work.

---

## Overview

This project started from a simple goal: have a place where I can experiment with realistic infrastructure without breaking anything that matters. Over time, it evolved into something closer to a compact enterprise lab.

The rack now includes:

- A Dell PowerEdge R710 as the main Proxmox host, with enough CPU and memory headroom to run realistic multi-VM scenarios.
- A pair of Dell EqualLogic FS7610 nodes and an Avid 18-bay storage chassis providing shared and bulk storage for virtual machines and data.
- A Dell X1052P managed switch, dual shielded patch panels, an OpenGear console manager, and a rackmount KVM for clean switching, structured cabling, and centralized out-of-band access.
- A Panasonic Toughbook CF-30 running NST/SELKS as a log sink, Suricata sensor, and SOC-style analysis console.

The goal is not just to power on hardware but to design and operate the environment as if it were a small, self-contained production network.

---

## Network & Segmentation

The environment is intentionally segmented to mirror a compact enterprise design. Management, core services, DMZ, lab workloads, honeypots, and guest devices each live on their own VLANs.

- The core switch provides Layer 2 separation.
- Inter-VLAN routing and policy enforcement are handled by the firewalls.
- Administrative interfaces are reachable exclusively from the management network.

In broad strokes:

- **Cisco ASA appliances** provide perimeter firewalling, NAT, and site-to-site or remote-access capabilities.
- **SonicWall SRA 4200** focuses on SSL VPN and remote access into the lab for administrative purposes.
- **Traffic between zones** is allowed only where it is explicitly needed, with defaults leaning toward deny + log.

This makes the lab a useful place to reason about real-world constraints: who should talk to whom, over what ports, and under which conditions.

---

## Security, Monitoring & Honeypots

Security and observability are treated as first-class design concerns rather than add-ons.

The SOC node:

- Ingests **firewall logs**, **host logs**, and **selected mirrored traffic** from the core switch and key firewall interfaces.
- Runs **Suricata** and the **SELKS stack** to provide visibility into what is happening on the wire.
- Acts as a place to tune detection rules and thresholds using real lab traffic.

Design principles:

- Important flows are mirrored and inspected at a **small number of well-chosen points** to avoid redundant processing and unnecessary complexity.
- A dedicated **honeypot zone** can be selectively exposed through the ASA to observe scan and attack patterns without risking production systems.
- Outbound traffic from honeypots and lab workloads is **tightly scoped and logged** to prevent unintended pivoting or abuse.

The result is an environment where experimentation with exposure, detection, and response can happen with guardrails in place.

---

## How This Repository Is Organized

This repository documents how the lab is assembled and how it is operated. It is structured so that someone who has never seen the physical rack can still understand the environment and reason about changes.

- `docs/` – High-level overview, hardware inventory, network and security architecture, services, operations, and future roadmap.
- `diagrams/` – Logical network diagram tying together zones, firewalls, and the core switch.
- `infra/` – Sanitized examples of an ASA base policy and placeholders for scripts or infrastructure-as-code concepts.
- `runbooks/` – Operational notes such as change history and, over time, backup and restore procedures.
- `assets/` – Space reserved for redacted photos of the rack and equipment.

The intent is that the documentation and structure make it possible to reconstruct the design and understand the reasoning behind it, not just the final state.

---

## Why This Lab Matters

Digital Fortress Lab is more than a collection of hardware; it is a long-running practice ground for infrastructure and security work.

Treating this environment like a small production network forces discipline:

- Changes are deliberate and recorded.
- Configuration is backed up and can be rebuilt.
- Design decisions are documented in version control instead of living only in memory.

The lab gives me a place to:

- Design around real constraints and trade-offs.
- Work through the balance between simplicity and flexibility.
- Practice habits that translate directly to professional environments: clear boundaries between zones, documented data flows, thoughtful placement of security controls, and observability built in from the beginning.

---

## Sanitization & Scope

All information in this repository is intentionally sanitized:

- IP ranges, hostnames, and object names are examples rather than live values.
- No keys, credentials, or VPN details are committed here.
- The lab is isolated from production or customer systems and is used strictly for personal education and experimentation.

Honeypot and exposure scenarios are designed to provide useful data without creating collateral risk.

In short, Digital Fortress Lab functions as both a **learning platform** and a **portfolio artifact**. It captures how I approach infrastructure and security in practice: start from clear boundaries, design the network as a system, build in observability from the start, and document enough that the environment can be understood, modified, and rebuilt by someone else.
