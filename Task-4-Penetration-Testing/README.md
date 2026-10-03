# Task 4 - Penetration Testing & System Security

## Overview

This project documents a controlled penetration testing and cybersecurity laboratory exercise performed using Kali Linux and Metasploitable2.

The lab covers reconnaissance, vulnerability identification, exploitation, password attacks, social engineering awareness, malware analysis, and system hardening.

> **Note:** All activities were performed in an authorized isolated virtual laboratory environment.

---

## Lab Environment

| Component | Details |
|---|---|
| Attacker / Analyst | Kali Linux |
| Target | Metasploitable2 |
| Target IP | 192.168.133.128 |
| Virtualization | VMware |
| Testing Scope | Local virtual lab |

---

## Objectives

The objectives of this lab were:

1. Exploit a known vulnerability in Metasploitable2 and obtain system access.
2. Perform post-exploitation activities and verify system information.
3. Perform password attacks using Hydra.
4. Crack password hashes using John the Ripper.
5. Perform a phishing-awareness simulation.
6. Study static and dynamic malware analysis using a benign sample.
7. Apply basic system-hardening techniques.

---

## Activities Performed

### 1. Reconnaissance and Nmap

Nmap was used to discover the target and identify open ports and services.

Important services identified included:

- FTP - TCP/21
- SSH - TCP/22
- Telnet - TCP/23
- HTTP - TCP/80
- SMB - TCP/139 and 445
- MySQL - TCP/3306
- Other legacy services

The scan revealed a large attack surface containing several outdated services.

---

### 2. Exploitation with Metasploit

The FTP service was identified as:

```text
vsftpd 2.3.4

The intentionally vulnerable vsftpd 2.3.4 backdoor vulnerability was exploited using Metasploit.

Module:

exploit/unix/ftp/vsftpd_234_backdoor

The exploitation resulted in root-level command access to the Metasploitable2 system.

Post-exploitation commands included:

whoami
id
hostname
uname -a

The session confirmed:

User: root
Hostname: metasploitable
Mitigation
Upgrade or remove vulnerable versions of vsftpd.
Disable FTP if it is not required.
Restrict FTP access using firewall rules.
Use secure alternatives such as SFTP.
Apply security patches regularly.
3. Password Attacks
Hydra

Hydra was used to perform a password audit against the target.

The successful lab test was performed against the FTP service because the legacy SSH service presented cryptographic compatibility issues with the current Hydra/OpenSSH configuration.

Successful result:

Login: msfadmin
Password: msfadmin
Service: FTP
Mitigation
Use strong and unique passwords.
Avoid default or predictable credentials.
Disable unused accounts.
Apply account lockout/rate-limiting controls where appropriate.
Restrict remote access to trusted hosts.
Use multi-factor authentication where supported.
4. John the Ripper

Password hashes obtained from the Metasploitable2 lab were combined using unshadow and tested with the rockyou.txt wordlist.

Three password hashes were successfully cracked:

Account	Password
sys	batman
klog	123456789
service	service

Result:

3 password hashes cracked
4 password hashes remained uncracked
Mitigation
Use strong and unique passwords.
Use secure password-hashing algorithms.
Protect /etc/shadow and other credential databases.
Use MFA where possible.
Avoid predictable passwords.
5. Social Engineering Simulation

A phishing-style security-awareness simulation was created.

The simulation:

Did not target real users.
Did not collect real credentials.
Did not collect OTPs.
Did not use a credential-harvesting form.
Focused on phishing detection and user awareness.
Awareness Measures

Users should:

Verify the sender before responding.
Check URLs before clicking.
Avoid entering credentials into suspicious pages.
Never share passwords or OTPs.
Report suspicious messages to the security team.
6. Malware Basics

A benign test sample was analyzed in a controlled Kali Linux environment.

Static Analysis

The sample was examined without executing malicious code.

Analysis included:

SHA-256 hash
File type
Strings

SHA-256:

d3db782c07bdf9471b1439cf59a8177cbfe70ceb2296139b89fa6fb1e8840bcd

File type:

ASCII text

Sample string:

BENIGN MALWARE ANALYSIS TEST SAMPLE
Dynamic Analysis

Before-and-after system observations were performed for:

Processes
Network connections
Files

No suspicious network activity or malware-related process was identified.

The exercise demonstrated the difference between static and dynamic malware analysis using a benign sample.

7. System Hardening
Security Patches

The Kali Linux system was updated using:

sudo apt update
sudo apt upgrade -y
Firewall

UFW was enabled and configured with:

Default: deny incoming
Default: allow outgoing
SSH: TCP/22 allowed
Disable Unused Services

The ModemManager service was identified as unnecessary for the VMware lab environment and was stopped and disabled.

Commands used:

sudo systemctl stop ModemManager
sudo systemctl disable ModemManager
Hardening Benefits
Reduces the attack surface.
Blocks unnecessary inbound traffic.
Removes unnecessary services.
Keeps software updated.
Improves overall system security.
Findings and Mitigations
Finding	Severity	Mitigation
vsftpd 2.3.4 vulnerable FTP service	Critical	Upgrade/remove vulnerable service
Weak FTP credentials	High	Use strong unique passwords
Recoverable weak passwords	High	Strong passwords and secure hashing
Legacy SSH service	High	Upgrade OpenSSH
Telnet exposed	High	Disable Telnet and use SSH
Legacy services	High	Patch and restrict unnecessary services
Unused ModemManager	Low	Disable unnecessary service
Unrestricted inbound traffic before hardening	Medium	Configure default-deny firewall
Repository Structure
Task-4-Penetration-Testing/
│
├── README.md
│
├── Exploitation/
│   └── Exploitation-Steps.md
│
├── Password-Attacks/
│   ├── Hydra-FTP.md
│   └── John-the-Ripper.md
│
├── Social-Engineering/
│   └── Social-Engineering-Simulation.md
│
├── Malware-Analysis/
│   └── Malware-Analysis.md
│
├── System-Hardening/
│   └── System-Hardening.md
│
└── Screenshots/
Conclusion

This laboratory demonstrated a complete controlled penetration-testing workflow, from reconnaissance and vulnerability identification to exploitation, password auditing, security awareness, malware analysis, and system hardening.

The exercise also demonstrated the importance of patching vulnerable software, using strong authentication, minimizing exposed services, configuring firewalls, and disabling unnecessary services.

All activities were performed in an authorized virtual laboratory environment.