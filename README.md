# 🛡️ Azure Sentinel SOC Home Lab
## Microsoft SIEM Honeypot — Real Attack Detection & SOAR Automation

![Attack Map](screenshots/attack-map.png)

## Overview
Built a live honeypot VM in Azure exposed to the public internet, ingested security logs into Microsoft Sentinel, and developed KQL detection rules, a geographic attack map, and automated SOAR playbooks responding to real-world threats.

- **Total attacks detected:** 200,000+ in 48 hours
- **Peak attack rate:** 15,000+ attempts per hour
- **Successful breaches:** Zero
- **Total project cost:** $6.75

---

## Architecture
- **Microsoft Azure** — Cloud infrastructure
- **Windows 11 Pro VM** — Honeypot exposed to internet
- **Log Analytics Workspace** — Central log database
- **Microsoft Sentinel** — SIEM/SOAR platform
- **Azure Monitor Agent** — Log collection pipeline
- **KQL** — Threat hunting and detection queries
- **Logic Apps** — SOAR automated response

---

## What I Built

### Phase 1 — Azure Environment
- Created Resource Group, Log Analytics Workspace
- Deployed Microsoft Sentinel connected to LAW

### Phase 2 — Honeypot VM
- Deployed Windows 11 Pro VM with public IP
- Disabled Windows Firewall and opened all NSG ports
- Installed Azure Monitor Agent for log forwarding
- Configured Data Collection Rule for Security Events

### Phase 3 — Threat Hunting & Attack Map
- Wrote KQL queries to analyze 200k+ attack events
- Built GeoIP watchlist to enrich attacker IPs with location
- Created live SOC-Attack-Map workbook in Sentinel

### Phase 4 — Detection Rules
- Created 4 scheduled analytics rules mapped to MITRE ATT&CK
- Rules triggered automatically on real attack data
- Generated 200,000+ incidents in 48 hours

### Phase 5 — SOAR Automation
- Built Logic Apps playbook triggered on incidents
- Automated email alerts with incident details
- Attached playbook to Brute Force detection rule

---

## Findings

### Attack Volume
The honeypot received **200,000+ failed RDP login attempts** within 48 hours of deployment, demonstrating how quickly exposed infrastructure is discovered and targeted.

### Top Attack Sources
| Country | Attempts |
|---------|----------|
| United States | 81,200 |
| Europe | 26,200 |
| China | 11,300 |
| Asia | 127 |
| South America | 57 |

### Peak Attack Times
Attack waves peaked between 7–8 PM and 1–2 AM UTC, suggesting coordinated botnet activity across multiple time zones.

### Most Targeted Usernames
Attackers primarily targeted default credentials:
`administrator` `admin` `root` `user` `guest` `postgres` `oracle` `ubuntu` `pi`

### Key Finding
Despite 200,000+ sustained brute force attempts across 48 hours from multiple countries, **zero successful unauthorized logins were recorded**, validating the detection and monitoring pipeline.

---

## Detection Rules

| Rule | Severity | Source | MITRE | Technique |
|------|----------|--------|-------|-----------|
| Brute Force Attack Detected | High | Custom | Initial Access | T1110 |
| Successful Login After Brute Force | High | Custom | Credential Access | T1110.001 |
| Suspicious User Account Created | Medium | Custom | Persistence | T1136 |
| User Added to Admin Group | High | Custom | Privilege Escalation | T1078 |
| Brute Force Against Azure Portal | High | Microsoft Entra | Credential Access | T1110 |
| Anomalous Sign-in Location | Medium | Microsoft Entra | Initial Access | T1078 |
| Account Created and Deleted | High | Microsoft Entra | Initial Access | T1078.004 |

## Active Directory Lab Addition

### Environment
- Windows Server 2022 Domain Controller (DC-01)
- Windows 11 Client joined to domain (Client-01)
- Domain: soclab.local
- 10 domain user accounts

### Attacks Simulated
| Attack | MITRE | Tool |
|--------|-------|------|
| Brute Force | T1110 | net use |
| Kerberoasting | T1558.003 | setspn |
| Credential Dumping | T1003 | Mimikatz |
| DCSync/Golden Ticket | T1003.006 | Mimikatz |
| Backdoor Account | T1136 | net user |
| Scheduled Task | T1053 | schtasks |
| Lateral Movement | T1021 | SMB |
| Password Spray | T1110.003 | PowerShell |

## KQL Queries
All detection and hunting queries available in [/kql-queries](kql-queries/)

---

## Screenshots

### Live Attack Map
![Attack Map](screenshots/attack-map.png)

### Analytics Rules Dashboard
![Analytics Rules](screenshots/analytics-rules.png)

### Active Incident
![Incident](screenshots/incident-alert.png)

### SOAR Email Alert
![SOAR Alert](screenshots/soar-email-alert.png)

### Attack Timeline
![Timeline](screenshots/attack-timeline.png)

---

## Tools Used
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoft-azure&logoColor=white)
![Sentinel](https://img.shields.io/badge/Microsoft_Sentinel-0078D4?style=flat&logo=microsoft&logoColor=white)
![KQL](https://img.shields.io/badge/KQL-blue?style=flat)
![Logic Apps](https://img.shields.io/badge/Logic_Apps-0078D4?style=flat&logo=microsoft-azure&logoColor=white)
