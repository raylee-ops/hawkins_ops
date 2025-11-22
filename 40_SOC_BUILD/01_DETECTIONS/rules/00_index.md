# HawkinsOps Detection Rules Index

## Rule Mapping Table

| Rule ID | MITRE ID | Technique | Platform | Severity | FP Risk |
|---------|----------|-----------|----------|----------|---------|
| 100100 | T1003.001 | LSASS Memory Dump | Windows | Critical | Low |
| 100101 | T1078.003 | Local Account Brute Force | Windows/Linux | High | Medium |
| 100102 | T1059.001 | Suspicious PowerShell Execution | Windows | High | Medium |
| 100103 | T1053.005 | Scheduled Task Created | Windows | Medium | Medium |
| 100104 | T1547.001 | Registry Run Keys Persistence | Windows | High | Low |
| 100105 | T1070.001 | Windows Event Log Cleared | Windows | High | Low |
| 100106 | T1562.001 | Defender Disabled | Windows | Critical | Low |
| 100107 | T1021.002 | SMB Lateral Movement | Windows | High | Medium |
| 100108 | T1003.003 | NTDS.dit Access | Windows | Critical | Low |
| 100109 | T1548.002 | UAC Bypass Attempt | Windows | High | Medium |
| 100110 | T1134.001 | Token Manipulation | Windows | High | Low |
| 100111 | T1110.001 | SSH Brute Force | Linux | High | Low |
| 100112 | T1078.003 | Multiple Failed Logins | Linux | Medium | Medium |
| 100113 | T1059.004 | Suspicious Bash Execution | Linux | Medium | High |
| 100114 | T1053.003 | Cron Job Created | Linux | Medium | Medium |
| 100115 | T1548.003 | Sudo Privilege Escalation | Linux | High | Medium |
| 100116 | T1070.006 | Linux Log Deletion | Linux | High | Low |
| 100117 | T1136.001 | New User Account Created | Windows/Linux | Medium | Low |
| 100118 | T1098.001 | Account Modification | Windows/Linux | Medium | Medium |
| 100119 | T1543.003 | Windows Service Created | Windows | Medium | Medium |
| 100120 | T1569.002 | Service Execution | Windows | Low | High |
| 100121 | T1087.001 | Account Discovery | Windows | Low | Medium |
| 100122 | T1082 | System Information Discovery | Windows/Linux | Low | High |
| 100123 | T1049 | Network Connection Enumeration | Windows/Linux | Low | High |
| 100124 | T1218.011 | Rundll32 Proxy Execution | Windows | High | Medium |
| 100125 | T1055.001 | Process Injection | Windows | Critical | Low |
| 100126 | T1105 | File Download via PowerShell | Windows | Medium | Medium |
| 100127 | T1071.001 | Web Service C2 Traffic | Windows/Linux | High | High |
| 100128 | T1027 | Obfuscated Command | Windows | Medium | Medium |
| 100129 | T1564.003 | Hidden Files/Directories | Linux | Low | Medium |

## Tuning Guide

### High False-Positive Rules (Tune First)
- **100113** (Suspicious Bash): Whitelist known admin scripts
- **100122** (System Info Discovery): Exclude monitoring tools
- **100127** (C2 Traffic): Requires network baseline; tune after 7 days

### Critical Rules (Alert Immediately)
- **100100** (LSASS Dump): Immediate investigation required
- **100106** (Defender Disabled): High confidence indicator
- **100108** (NTDS.dit): Domain compromise indicator

---
**Last Updated:** 2025-11-22 | **Total Rules:** 30
