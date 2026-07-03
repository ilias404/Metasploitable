# 🛡️ Metasploitable 2 — Security Audit & Remediation

Academic penetration testing project conducted as part of the **Sécurité des Systèmes d'Information** module at **ENSA Oujda** (MGSI, 4th year).

The goal was to perform a complete offensive/defensive security audit on **Metasploitable 2**, a deliberately vulnerable Linux VM, following a full pentest methodology: reconnaissance → scanning → vulnerability analysis → exploitation (PoC) → remediation planning.

⚠️ **Educational use only.** All testing was performed in a fully isolated Host-only lab network, with no connection to production systems or the internet.

---

## 📋 Project Info

|  |  |
| :---- | :---- |
| **Institution** | École Nationale des Sciences Appliquées d'Oujda |
| **Program** | MGSI — 4th year |
| **Module** | Sécurité des Systèmes d'Information |
| **Supervisor** | M. Mohammed OUADOUD |
| **Academic year** | 2025–2026 |
| **Report version** | v1.0 — 25/04/2026 |

**Team**

- AMRANI Ilias  
- BOUAZZAOUI Younes  
- RHOUL Rayane  
- TAIBI Abdessamad  
- LASRI Yassir

---

## 🧪 Lab Environment

|  |  |
| :---- | :---- |
| Target | Metasploitable 2 (`192.168.159.128`) |
| Attacker | Kali Linux (`192.168.159.129`) |
| Network | Host-only VMware (`192.168.159.0/24`) |
| Hypervisor | VMware Workstation on Windows 11 |

## 🔧 Tools Used

`nmap` · `Metasploit Framework` · `enum4linux` · `gobuster` · `rpcclient` · `netcat` · `curl` · `cadaver` · `smbclient` · `showmount` · `vncviewer`

---

## 🔍 Methodology

1. **Reconnaissance** — host discovery on the lab subnet  
2. **Scanning & Identification** — full TCP port sweep (1–65535) \+ service/version detection  
3. **Vulnerability Analysis** — 33 exposed services/applications analyzed and exploited (PoC)  
4. **Remediation / Hardening** — prioritized correction plan (quick wins vs. structural fixes)  
5. **Final Verification** — before/after comparison of the security posture

---

## 🎯 Scope

- Full TCP port range (1–65535) on Metasploitable 2  
- Network services (FTP, SSH, Telnet, Samba, RPC, NFS, MySQL, PostgreSQL, VNC, IRC, etc.)  
- Web applications hosted on the target (**DVWA**, **Mutillidae**, phpMyAdmin)  
- Default system accounts

**Out of scope:** DoS testing, social engineering, physical attacks, real data exfiltration, exhaustive UDP scanning.

---

## 🚨 Key Findings

**32 vulnerabilities** identified and documented — **14 Critical**, **12 High**, **6 Medium**.

| Category | Examples |
| :---- | :---- |
| Backdoored software | vsftpd 2.3.4, UnrealIRCd 3.2.8.1, exposed root BindShell (1524) |
| Unencrypted protocols | Telnet, FTP, r-services (rexec/rlogin/rsh) |
| Default / weak credentials | MySQL root, PostgreSQL, VNC (`password`), Tomcat Manager, DVWA (`admin/password`), ProFTPD |
| Unauthenticated exposure | NFS root export (`*`), Java RMI, distccd, WebDAV upload, SMB/RPC null sessions |
| OWASP Top 10 (web apps) | SQL Injection, OS Command Injection, Reflected & Stored XSS, LFI, CSRF, Unrestricted File Upload, Clickjacking |

Each finding includes: description, affected asset, PoC evidence, exploitability, CIA impact, severity, root cause, and remediation.

### Notable CVEs exploited

`CVE-2007-2447` (Samba usermap script) · `CVE-2010-2075` (UnrealIRCd backdoor) · `CVE-2007-3280` (PostgreSQL RCE) · `CVE-2020-1938` (Ghostcat) · `CVE-2012-1823` (PHP CGI arg injection) · `CVE-2004-2687` (distccd RCE)

---

## 🛠️ Remediation Plan

Corrections were split into two tracks (see full report, Section 8):

- **Immediate fixes** (low effort, high impact): disable BindShell, r-services, Telnet, FTP; kill the backdoored IRC service; restrict/disable NFS.  
- **Structural fixes**: rotate default credentials, patch outdated services (SSH, Samba, PHP, PostgreSQL, Tomcat), enforce SMB signing, sanitize all web app inputs, add anti-CSRF tokens, apply security headers (`X-Frame-Options`, CSP).

A full before/after comparison table and per-service remediation detail is included in the report.

---


## 📖 Report Contents

The full PDF report (86 pages) includes:

- Context, scope, and ethical/legal rules  
- Reconnaissance and scanning methodology (Nmap outputs)  
- Detailed analysis of all 33 exposed services  
- Full vulnerability inventory & severity matrix  
- 32 individually documented vulnerability sheets (VULN-01 → VULN-32/33)  
- Prioritized remediation and hardening plan  
- Before/after verification summary  
- Conclusion & lessons learned

---

## ⚖️ Disclaimer

This project was carried out strictly for educational purposes on an intentionally vulnerable virtual machine, in an isolated lab network. No real-world systems were targeted. Metasploitable 2 must never be exposed to an untrusted network.

