# 🔐 SOC Incident Investigation using Splunk SIEM

![Tool](https://img.shields.io/badge/Tool-Splunk-FF6600?style=for-the-badge&logo=splunk&logoColor=white)
![Type](https://img.shields.io/badge/Type-SOC%20L1%20Simulation-blue?style=for-the-badge)
![Technique](https://img.shields.io/badge/MITRE-T1110%20Brute%20Force-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **Simulated a complete SOC L1 analyst investigation** — ingested real Linux authentication logs into Splunk, built custom SPL queries to detect brute-force attack patterns, identified suspicious IPs, and documented findings as a formal incident report.

---

## 🎯 Objective

Replicate a real-world SOC Level 1 analyst workflow using Splunk SIEM:
- Ingest and index authentication logs
- Build SPL queries to detect attack patterns
- Identify attacker IPs and compromised accounts
- Produce a structured incident investigation report

---

## 🛠️ Tools & Environment

| Component | Details |
|---|---|
| **SIEM Platform** | Splunk Enterprise (Free Trial) |
| **Log Source** | Linux Authentication Logs (`auth.log`) |
| **Query Language** | SPL (Search Processing Language) |
| **Attack Type Detected** | Brute-Force (T1110) |
| **OS** | Windows (Splunk hosted locally) |

---

## 📋 Investigation Methodology

### Phase 1 — Log Ingestion
```
Splunk → Settings → Add Data → Upload
→ Selected: Linux auth.log file
→ Source type: linux_secure
→ Index: main
```

### Phase 2 — SPL Queries Built

**Query 1 — View all ingested logs:**
```spl
index=main
```

**Query 2 — Detect all failed login attempts:**
```spl
index=main "Failed password"
```

**Query 3 — Identify top suspicious source IPs:**
```spl
index=main "Failed password"
| stats count by src_ip
| sort -count
```

**Query 4 — Detect brute-force threshold (10+ failures):**
```spl
index=main "Failed password"
| stats count by src_ip
| where count > 10
| sort -count
```

**Query 5 — Identify targeted usernames:**
```spl
index=main "Failed password"
| rex "Failed password for (?<username>\S+)"
| stats count by username
| sort -count
```

**Query 6 — Timeline of attack activity:**
```spl
index=main "Failed password"
| timechart count by src_ip
```

---

## 🔍 Key Findings

| # | Finding | Severity | Evidence |
|---|---|---|---|
| 1 | Single IP with 50+ failed logins in 5 minutes | 🔴 Critical | Brute-force attack confirmed |
| 2 | Root account targeted repeatedly | 🔴 Critical | Privilege escalation attempt |
| 3 | Attack occurred between 02:00–03:00 AM | 🟡 Medium | Off-hours activity |
| 4 | Multiple usernames tried from same IP | 🔴 High | Credential stuffing pattern |

---

## 🛡️ MITRE ATT&CK Mapping

| Tactic | Technique | ID | Evidence |
|---|---|---|---|
| Credential Access | Brute Force: Password Guessing | T1110.001 | 50+ failed SSH attempts |
| Initial Access | Valid Accounts | T1078 | Root account targeted |
| Discovery | System Owner/User Discovery | T1033 | Multiple username enumeration |

---

## 📊 Investigation Screenshots

> Screenshots in `/screenshots` folder:
> - `splunk-data-upload.png` — Log ingestion into Splunk
> - `splunk-all-logs-view.png` — All logs indexed
> - `splunk-failed-login-detection.png` — Failed password query results
> - `splunk-suspicious-ip-detection.png` — Top attacker IPs identified

---

## 📄 Incident Report

Full structured investigation report:
👉 [`investigation-report.md`](investigation-report.md)

---

## 💡 Skills Demonstrated

- ✅ Splunk log ingestion & indexing
- ✅ SPL query construction (stats, rex, timechart, where)
- ✅ Brute-force attack detection
- ✅ Attacker IP identification & analysis
- ✅ MITRE ATT&CK framework mapping
- ✅ SOC L1 incident investigation workflow
- ✅ Formal incident report writing

---

## 🔗 Related Projects

| Project | Description |
|---|---|
| [Wireshark Network Analysis](https://github.com/vivek-sh45/wireshark-network-traffic-analysis) | Packet-level threat detection |
| [Nmap Vulnerability Scan Lab](https://github.com/vivek-sh45/nmap-vulnerability-scan-lab) | Network reconnaissance & scanning |
| [Threat Hunting Lab](https://github.com/vivek-sh45/threat-hunting-lab) | Proactive threat hunting with Wireshark |

---

## 👤 Author

**Vivek Sharma** — Cybersecurity Analyst (Fresher) | SOC Operations

[![LinkedIn](https://img.shields.io/badge/LinkedIn-vivek--sharma--cybersec-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/vivek-sharma-cybersec)
[![GitHub](https://img.shields.io/badge/GitHub-vivek--sh45-181717?style=flat&logo=github)](https://github.com/vivek-sh45)
[![Email](https://img.shields.io/badge/Email-thecybervivek@gmail.com-D14836?style=flat&logo=gmail)](mailto:thecybervivek@gmail.com)
