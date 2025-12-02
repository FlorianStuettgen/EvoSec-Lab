# Digital Infrastructure Lab

<div align="center">
  <img src="/assets/photos/test2.jpeg" alt="Enterprise Rack Configuration" width="75%" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
</div>

<div align="center" style="margin-top: 16px;">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat&logo=proxmox&logoColor=white" alt="Lab Status: Active"/>
  <img src="https://img.shields.io/badge/Built-Solo-1182c3?style=flat&logo=github&logoColor=white" alt="Built Solo"/>
  <img src="https://img.shields.io/badge/Documentation-Comprehensive-ff8800?style=flat&logo=markdown&logoColor=white" alt="Comprehensive Documentation"/>
  <img src="https://img.shields.io/badge/Nerd_Factor-11/10-ff0066?style=flat&logo=dependabot&logoColor=white" alt="Nerd Factor"/>
</div>

<details open>
<summary><strong>Introduction</strong></summary>

This repository details the architecture, implementation, and management of a dedicated digital infrastructure laboratory. Built on genuine enterprise hardware, it provides a secure, isolated environment for designing, testing, and refining network topologies, security measures, and operational frameworks.

</details>

> [!IMPORTANT]  
> Engineered with production-level standards on authentic hardware, accompanied by exhaustive documentation to support professional development and portfolio enhancement.

> [!NOTE]  
> Operated in complete isolation from production environments to enable risk-free experimentation with realistic scenarios.

## At a Glance — Current as of December 2025

<div align="center" style="margin-bottom: 20px; font-style: italic; color: #666;">
  A concise overview of the lab's key components and their configurations.
</div>

<details>
<summary><strong>Hypervisor</strong> — Proxmox VE on Dell R710 (128 GB RAM, dual Xeon)</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Stable</p>
  <p>This core virtualization platform ensures efficient resource allocation and high availability.</p>
</div>
</details>

<details>
<summary><strong>Storage</strong> — Dual EqualLogic FS7610 + Avid 18-bay chassis</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Redundant</p>
  <p>Provides robust, fault-tolerant storage solutions for data integrity and performance.</p>
</div>
</details>

<details>
<summary><strong>Core Switch</strong> — Dell X1052P (52-port, full VLAN trunking)</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> L2 Master</p>
  <p>Serves as the central networking hub with advanced Layer 2 capabilities.</p>
</div>
</details>

<details>
<summary><strong>Perimeter</strong> — Cisco ASA 5510/5515-X + SonicWall SRA 4200</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Hardened</p>
  <p>Fortifies the lab's boundaries with enterprise-grade firewall and remote access security.</p>
</div>
</details>

<details>
<summary><strong>SOC Node</strong> — Panasonic Toughbook (NST/SELKS + Suricata)</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Live DPI</p>
  <p>Enables real-time security operations and deep packet inspection.</p>
</div>
</details>

<details>
<summary><strong>Network Model</strong> — Multi-zone, ASA-only L3 routing</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Zero Trust–inspired</p>
  <p>Implements segmented, secure networking principles for enhanced control.</p>
</div>
</details>

<details>
<summary><strong>OOB Management</strong> — OpenGear CM4148 + rack KVM + HP TFT5600</summary>
<div style="padding: 10px; background-color: #f9f9f9; border-left: 4px solid #0078d4; border-radius: 4px;">
  <p><strong>Status:</strong> Always reachable</p>
  <p>Ensures out-of-band access for reliable management and troubleshooting.</p>
</div>
</details>

<div align="center" style="margin-top: 30px;">
  <strong>Lab Maturity</strong><br>
  <progress value="94" max="100" style="width: 60%; height: 24px; border-radius: 4px;"></progress> <span style="font-weight: bold; font-size: 1.1em; margin-left: 10px;">94%</span>
</div>

<details>
<summary><strong>System Architecture Diagram (Mermaid)</strong></summary>

```mermaid
graph TD
    A[Hypervisor: Proxmox VE] --> B[Storage: EqualLogic FS7610]
    A --> C[Core Switch: Dell X1052P]
    C --> D[Perimeter: Cisco ASA]
    D --> E[SOC Node: Suricata]
    A --> F[Network Model: Zero Trust]
    G[OOB Management: OpenGear] --> A
    style A fill:#e6f3ff,stroke:#0078d4
    style B fill:#e6f3ff,stroke:#0078d4
    style C fill:#e6f3ff,stroke:#0078d4
    style D fill:#e6f3ff,stroke:#0078d4
    style E fill:#e6f3ff,stroke:#0078d4
    style F fill:#e6f3ff,stroke:#0078d4
    style G fill:#e6f3ff,stroke:#0078d4


































































































## Table of Contents

<details open>
<summary><strong>Click sections to collapse/expand</strong></summary>

- [Purpose & Philosophy](#purpose--philosophy)
- [Physical Platform Gallery](#physical-platform-gallery)
- [Logical Architecture & Zones](#logical-architecture--zones)
- [Mermaid Traffic Flow Masterpiece](#mermaid-traffic-flow)
- [Security & Observability Stack](#security--observability)
- [Repository Structure](#repository-structure)
- [Professional Impact](#professional-impact)
- [Operations Discipline](#operations-discipline)
- [100% Solo Operator](#solo-operator)
- [Sanitization & Safety](#sanitization--safety)

</details>

## Purpose & Philosophy

This lab exists to **break things safely, document everything, and level-up**.

- Model real enterprise networks at 1/1000th the cost  
- Prototype firewall policies that survive red-team scrutiny  
- Feed honeypots to the internet and reverse-engineer attacks  
- Practice change management as if auditors were watching  
- Build observability that actually works  

~~A rack of old gear~~ → **A living, breathing portfolio masterpiece**

**Key Definitions**  
**Lab** :: Controlled environment for high-signal R&D  
**Operator** :: One human, infinite coffee  
**End State** :: Reproducible from this repo in <48 hours

## Physical Platform — Rack Porn Gallery

<details open>
<summary><strong>Compute & Storage</strong> — Click to collapse</summary>
<br>
<img src="/assets/photos/Compute1.jpg" alt="R710" loading="lazy" width="100%"/>
<img src="/assets/photos/Compute2.png" alt="EqualLogic" loading="lazy" width="100%"/>
<img src="/assets/photos/Storage1.png" alt="Avid" loading="lazy" width="100%"/>
</details>

<details>
<summary><strong>Network & OOB Management</strong></summary>
<br>
<img src="/assets/photos/switch.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/patch.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/console3.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/console1.jpg" loading="lazy" width="100%"/>
</details>

<details>
<summary><strong>Security & SOC Node</strong></summary>
<br>
<img src="/assets/photos/sec1.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/sec3.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/sec2.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/monitor1.jpg" loading="lazy" width="100%"/>
<img src="/assets/photos/monitor2.jpg" loading="lazy" width="100%"/>
</details>

## Logical Architecture & Zones

| Zone       | Trust     | Color | Purpose                              |
|------------|-----------|-------|--------------------------------------|
| Management | Highest   | Blue  | Crown jewels & consoles              |
| Core       | High      | Green | Proxmox + storage                    |
| DMZ        | Medium    | Yellow| Controlled exposure                  |
| Lab        | Medium    | Orange| General workloads                    |
| Honeypots  | Low       | Red   | Attack surface bait                  |
| Guest      | Lowest    | Black | Untrusted devices                    |

### Traffic Flow — Mermaid Masterpiece

```mermaid
graph TD
    subgraph "Internet"
        EXT[Internet<br>Scans • Bots • Script Kiddies] 
    end
    subgraph "Perimeter"
        ASA[ASA Outside<br>Cisco Firepower]
        SRA[SonicWall SRA<br>VPN Gateway]
    end
    subgraph "Trusted"
        MGMT[Management Zone]
        CORE[Core Zone]
        DMZ[DMZ Zone]
        LAB[Lab Zone]
        HONEY[Honeypots]
        GUEST[Guest Zone]
    end
    subgraph "Observability"
        SOC[SOC Node<br>Suricata + SELKS]
    end

    EXT -->|Controlled| ASA
    ASA --> DMZ & CORE & LAB & GUEST
    ASA --> SRA --> MGMT
    HONEY --> ASA
    SOC -.->|SPAN + Syslog| ASA & DMZ & HONEY

    classDef danger fill:#ff5555,stroke:#c00,color:white
    classDef secure fill:#55ff55,stroke:#080,color:black
    classDef neutral fill:#5555ff,stroke:#00c,color:white
    class EXT,HONEY danger
    class MGMT,CORE secure
    class DMZ,LAB,GUEST,SRA neutral
    class SOC fill:#ffff55,stroke:#aa0,color:black

## Repository Structure

```bash
digital-infrastructure-lab/
├── docs/                  # Architecture deep-dives & runbooks
├── diagrams/              # Mermaid + exported Visio diagrams
├── infra/                 # Sanitized ASA configs + Ansible samples
├── runbooks/              # Change log, procedures, rollback plans
└── assets/
    └── photos/            # The rack beauty you’re enjoying right now
Recommended starting point → docs/00_overview.md


### Block 9 – Professional Impact (Portfolio Gold)

```markdown
## Professional Impact — This Is Portfolio Gold

| Discipline                | Real-World Skills Demonstrated                                      |
|---------------------------|---------------------------------------------------------------------|
| Network Engineering       | Zone-based firewall design, ASA object-group mastery, VLAN architecture |
| Security Engineering      | Suricata IDS tuning, honeypot deployment, attack traffic analysis   |
| SRE / Platform Engineering| Full-stack observability, reproducibility, runbook discipline       |
| DevOps & Automation       | Ansible playbooks, config-as-code, documentation-as-code            |
| Technical Leadership      | End-to-end ownership, systems thinking, risk-aware design          |

> This single repository has replaced entire “homelab” sections on résumés.  
> Recruiters and senior engineers stop scrolling when they land here.

## 100% Solo Operator

Every cable pulled, every ACL written, every diagram drawn, every line of Markdown — **one human**.

- Sourced and refurbished all enterprise hardware  
- Designed every security zone and policy from scratch  
- Stood up Proxmox, ASA, SonicWall, Suricata, SELKS  
- Authored the entire documentation suite and runbooks  
- Still adding features at 2 a.m. because it’s fun

<p align="center">
  <strong>Built with precision.<br>Documented with obsession.<br>Operated with fire.</strong>
  <br><br>
  <img src="https://img.shields.io/badge/Level-Over_9000-ff0066?style=for-the-badge&logo=dependabot" alt="Over 9000"/>
  <br><br>
  <a href="#digital-infrastructure-lab">Back to Top</a>
</p>




















