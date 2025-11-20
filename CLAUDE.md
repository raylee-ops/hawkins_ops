# CLAUDE.md - AI Assistant Guide for HawkinsOps

**Version:** 1.0
**Last Updated:** 2025-11-20
**Repository:** hawkins_ops (raylee-ops)

---

## 🎯 PROJECT OVERVIEW

**HawkinsOps** is a **production-grade personal Security Operations Center (SOC)** training environment designed to demonstrate enterprise-level security operations capabilities for SOC analyst positions.

### Project Purpose
- **Owner:** Raylee
- **Career Goal:** Tier 1 SOC Analyst → Cloud/IAM/OT Security
- **Hire-Ready Target:** May 1, 2026
- **Status:** Serious enterprise-grade training environment (NOT a toy lab)
- **Use Case:** Job interview proof-of-capability + ongoing security operations training

### Infrastructure Scope
- Multi-node SOC environment with:
  - Windows 11 Powerhouse (analyst workstation + monitoring)
  - Linux Mint PRIMARY_OS (operations server)
  - Proxmox virtualization cluster
  - pfSense firewall/router
  - Wazuh SIEM (manager + agents)
  - Active Directory domain services
  - Multiple Windows/Linux monitored endpoints

---

## 📁 REPOSITORY STRUCTURE

```
/home/user/hawkins_ops/
├── blueprints/               # Complete rebuild documentation
│   └── rebuild_pack/         # 8 comprehensive rebuild guides
│       ├── 00_index.md       # [CRITICAL] Master index & navigation
│       ├── assumptions.md    # [CRITICAL] 25 critical assumptions
│       ├── 01_hawkinsops_high_level_architecture.md
│       ├── 02_rebuild_master_runbook.md  # Complete rebuild procedure
│       ├── 10_windows_powerhouse_rebuild.md
│       ├── 20_primary_os_rebuild_overview.md
│       ├── 30_services_matrix.md         # Service inventory & health checks
│       └── 40_sample_scripts_and_snippets.md  # 34 code examples
├── data/
│   ├── archives/             # Archived operational data
│   ├── logs/                 # Mirror sync logs (18+ files)
│   ├── notes/                # Working notes
│   └── reports/              # System reports (Phase_2_Report.md)
├── system/
│   ├── config/               # Configuration files
│   ├── scripts/              # Automation scripts
│   │   └── autosync.ps1     # Daily backup & Git sync
│   └── templates/            # Script/config templates
├── vault/                    # Sensitive data (credentials, finance)
│   ├── finances/
│   ├── personal/
│   └── projects/
└── workspace/                # Day-to-day working files
    ├── active/
    ├── reference/
    └── temp/
```

### Directory Purposes

| Directory | Purpose | AI Assistant Notes |
|-----------|---------|-------------------|
| `blueprints/` | Complete disaster recovery documentation | **READ FIRST** - Contains all architectural knowledge |
| `data/` | Operational logs, reports, notes | Check here for system status history |
| `system/` | Automation scripts and configs | Core automation logic lives here |
| `vault/` | Sensitive data storage | **DO NOT** commit credentials or sensitive data |
| `workspace/` | Working files and references | Temporary work area |

---

## 🔑 CRITICAL FILES - MUST READ

### Documentation (blueprints/rebuild_pack/)

1. **`assumptions.md`** - **[CRITICAL]** Read FIRST before any infrastructure changes
   - 25 critical assumptions about network, domain, IPs, credentials
   - Network: `192.168.50.0/24`
   - Domain: `hawkinsops.local`
   - Contains IP assignments, versions, hardware requirements

2. **`00_index.md`** - Master navigation guide
   - Reading order for first-time readers
   - Scenario-based navigation (disaster recovery, component rebuild)
   - Estimated rebuild time: 8-12 hours

3. **`01_hawkinsops_high_level_architecture.md`** - Complete architecture
   - Component hierarchy (physical + virtual layers)
   - Network architecture (VLANs, IP assignments, routing)
   - Data flow diagrams
   - Service dependencies
   - **Reference this** when making infrastructure recommendations

4. **`02_rebuild_master_runbook.md`** - Complete rebuild procedure (907 lines)
   - 12 phases from bare metal to operational
   - Phase-by-phase checkpoints and verification
   - Troubleshooting guide
   - Emergency rollback procedures
   - **Use this** for understanding deployment workflows

5. **`30_services_matrix.md`** - Service inventory & health monitoring
   - 10 hosts with detailed service mappings
   - Health check scripts (PowerShell & Bash)
   - Service dependency map
   - Expected baseline metrics
   - **Reference this** before modifying services

6. **`40_sample_scripts_and_snippets.md`** - 34 code examples
   - PowerShell scripts (Windows hardening, Wazuh deployment)
   - Bash scripts (Linux hardening, SSH config)
   - Wazuh configuration examples
   - **Use these patterns** when writing new scripts

### Automation Scripts

1. **`system/scripts/autosync.ps1`** - Daily automated backup
   - Mirrors C:\HAWKINS_OPS to D:\Backups using robocopy
   - Auto-commits to Git with timestamp
   - Scheduled daily at 23:00 via Windows Task Scheduler
   - **DO NOT** modify without understanding backup workflow

---

## 💻 TECH STACK

### Operating Systems
- Windows 11 Pro (analyst workstation)
- Windows Server 2022 (Active Directory DC)
- Linux Mint 21.x (operations server & endpoints)
- Ubuntu 22.04 LTS (Wazuh SIEM)
- Proxmox VE 8.x (virtualization)
- pfSense 2.7.x (firewall/router)

### Security & Monitoring
- **Wazuh 4.x** - SIEM platform (manager + agents)
- **Sysmon** - Windows process monitoring
- **Auditd** - Linux audit daemon
- **Windows Defender** - Endpoint protection
- **UFW** - Linux firewall

### Scripting & Automation
- **PowerShell 7.5.4** - Windows automation (primary scripting language)
- **Bash** - Linux scripting
- **Python 3** - Advanced scripting
- **Git 2.51.2** - Version control

### Networking
- **Active Directory DS** - Domain services & DNS
- **pfSense** - Gateway, routing, VLANs, NAT, firewall
- **Samba/SMB** - File sharing

---

## 🔄 DEVELOPMENT WORKFLOWS

### Version Control Strategy

**Current Setup:**
- **Remote Repository:** GitHub (raylee-ops/hawkins_ops)
- **Primary Working Copy:** Windows Powerhouse (`C:\HAWKINS_OPS`)
- **Mirror Copy:** PRIMARY_OS Linux (`/home/raylee/HAWKINS_OPS/`)
- **Current Branch:** `claude/claude-md-mi6r7ob1yqwc12hv-018ugndqfe5F6c9DgWojB1Nr`

**Automated Git Workflow:**
1. Daily autosync.ps1 runs at 23:00
2. Commits with message: `"Auto-sync: YYYY-MM-DD HH:mm:ss"`
3. Pushes to GitHub automatically

**AI Assistant Git Practices:**
- ✅ **DO:** Work on the designated branch (starts with `claude/`)
- ✅ **DO:** Write clear, descriptive commit messages for manual commits
- ✅ **DO:** Push to remote using: `git push -u origin <branch-name>`
- ✅ **DO:** Retry failed pushes up to 4 times with exponential backoff (2s, 4s, 8s, 16s)
- ❌ **DON'T:** Push to branches not starting with `claude/` without permission
- ❌ **DON'T:** Force push to main/master
- ❌ **DON'T:** Modify autosync.ps1 without explicit request

### Backup Strategy (3-Tier)

1. **Primary Backup:** Daily robocopy mirror to `D:\Backups\HAWKINS_OPS`
2. **Secondary Backup:** Git push to GitHub
3. **Tertiary Backup:** Manual sync to PRIMARY_OS Linux via Samba share

**Logs:** Stored in `data/logs/mirror_YYYYMMDD_HHMMSS.log`

### File Management Workflow

**Creating New Files:**
- Documentation → `blueprints/` (Markdown format)
- Scripts → `system/scripts/` (PowerShell or Bash)
- Reports → `data/reports/` (Markdown format)
- Temporary work → `workspace/temp/`

**Modifying Existing Files:**
- Always read the file first before editing
- Preserve existing formatting and style
- Add version/update notes if modifying critical docs
- Test scripts before committing

---

## 📋 CONVENTIONS & PATTERNS

### Naming Conventions

**Hostnames:**
- Format: `function-identifier` (lowercase with hyphens)
- Examples: `win-powerhouse`, `primary-os`, `mint-3`
- FQDN: `hostname.hawkinsops.local`

**Files:**
- Documentation: `00_index.md`, `01_architecture.md` (numbered for reading order)
- Logs: `mirror_YYYYMMDD_HHMMSS.log` (ISO date format)
- Scripts: `autosync.ps1`, `health_check.sh` (descriptive, lowercase with underscores)

**Directories:**
- Structure dirs: `rebuild_pack`, `primary_os` (lowercase with underscores)
- Main structure: `HAWKINS_OPS` (uppercase for visibility)

### Documentation Patterns

**Markdown Structure:**
```markdown
# H1 - Document Title
## H2 - Major Sections
### H3 - Subsections

**Emphasis** for important terms
`code` for commands/file paths
```bash
code blocks with language specifiers
```

**CHECKPOINT:** Verification steps
[CRITICAL] - Cannot skip
[IMPORTANT] - Recommended
```

**Runbook Format:**
```markdown
## Phase X: Description
### X.1 Substep Name
1. Numbered sequential instructions
2. Commands in code blocks
3. Expected output documented
4. **CHECKPOINT:** Verification command with expected result

### X.2 Next Substep
...

## Troubleshooting
Common issues and solutions
```

### PowerShell Conventions

```powershell
# Use approved verbs (Get-, Set-, New-, Test-, etc.)
# Clear variable names in UPPERCASE for configuration
$WAZUH_MANAGER = "192.168.50.10"
$AGENT_NAME = $env:COMPUTERNAME

# Comments explaining purpose
# Health check for Wazuh agent status

# Error handling in production scripts
try {
    Start-Service -Name "WazuhSvc"
} catch {
    Write-Error "Failed to start Wazuh service: $_"
}

# Output for verification
Write-Host "Wazuh agent enrolled successfully" -ForegroundColor Green
```

### Bash Conventions

```bash
#!/bin/bash
# Set safety flags
set -e  # Exit on error

# UPPERCASE for configuration variables
WAZUH_MANAGER="192.168.50.10"
AGENT_NAME=$(hostname)

# Echo status with color codes
echo -e "\e[32m[SUCCESS]\e[0m Wazuh agent installed"
echo -e "\e[31m[ERROR]\e[0m Service failed to start"

# Clear function names
check_service_status() {
    systemctl is-active --quiet "$1"
}
```

### Security Patterns

**Defense in Depth:**
- Network firewall (pfSense) + host firewalls (Windows Firewall, UFW)
- Monitoring at every layer → all logs forwarded to Wazuh SIEM
- Multiple authentication layers (local + domain + SIEM)

**Least Privilege:**
- Separate user and admin accounts
- Service accounts with minimal permissions
- Firewall rules: default deny, explicit allow

**Audit Everything:**
- PowerShell logging (module, script block, transcription)
- Windows audit policies enabled
- Linux auditd on sensitive files
- Sysmon for process execution
- All logs → Wazuh for correlation

**Assume Breach:**
- SIEM monitoring all hosts 24/7
- Detection rules for lateral movement (MITRE ATT&CK aligned)
- File integrity monitoring on critical files
- Network segmentation via pfSense VLANs

---

## 🤖 AI ASSISTANT GUIDELINES

### When Working with This Repository

**ALWAYS:**
1. **Read `assumptions.md` FIRST** before suggesting infrastructure changes
2. **Reference architecture docs** before modifying network/service configs
3. **Use existing code patterns** from `40_sample_scripts_and_snippets.md`
4. **Test suggestions** against documented IP ranges and domain names
5. **Preserve documentation structure** (numbered files, checkpoint format)
6. **Check service dependencies** in `30_services_matrix.md` before changes
7. **Commit with clear messages** describing what and why
8. **Push to correct branch** (must start with `claude/`)

**NEVER:**
1. ❌ Suggest changes that violate assumptions.md (IP ranges, domain names, etc.)
2. ❌ Commit credentials, passwords, or sensitive data to Git
3. ❌ Modify autosync.ps1 without explicit user request
4. ❌ Push to main/master or force push
5. ❌ Delete or rename numbered documentation files without permission
6. ❌ Suggest infrastructure changes without checking architecture docs
7. ❌ Write scripts that bypass security controls (firewalls, logging, etc.)

### Understanding Infrastructure Context

**Network Configuration:**
- Lab Network: `192.168.50.0/24`
- Management Network: `192.168.10.0/24`
- Domain: `hawkinsops.local`
- DNS Server: `192.168.50.20` (AD DC)
- Gateway: `192.168.50.1` (pfSense)

**Key IP Assignments:**
| Host | IP | Role |
|------|----|----- |
| pfSense LAN | 192.168.50.1 | Gateway |
| Wazuh Manager | 192.168.50.10 | SIEM |
| DC01 | 192.168.50.20 | Domain Controller |
| PRIMARY_OS | 192.168.50.100 | Operations Server |
| WIN-POWERHOUSE | 192.168.50.101 | Analyst Workstation |
| MINT-3 | 192.168.50.102 | Monitored Endpoint |

**Service Dependencies (Critical Path):**
1. Proxmox hypervisor (foundation)
2. pfSense (network routing & DNS forwarding)
3. Active Directory DC (DNS, authentication)
4. Wazuh Manager (SIEM, log aggregation)
5. Endpoints (Windows & Linux agents)

### Common Tasks for AI Assistants

#### Task: Update Documentation

```bash
# 1. Read the existing file first
# 2. Make changes preserving structure
# 3. Update "Last Updated" date if present
# 4. Commit with clear message
git add blueprints/rebuild_pack/XX_filename.md
git commit -m "Updated XX_filename.md: [brief description of changes]"
git push -u origin claude/claude-md-<session-id>
```

#### Task: Create New Script

```bash
# 1. Determine correct location
#    - Windows automation → system/scripts/*.ps1
#    - Linux automation → system/scripts/*.sh
# 2. Follow language conventions (see above)
# 3. Add comments explaining purpose
# 4. Include error handling
# 5. Test before committing
# 6. Add to 40_sample_scripts_and_snippets.md if reusable

git add system/scripts/new_script.ps1
git commit -m "Added new_script.ps1: [purpose description]"
git push -u origin claude/claude-md-<session-id>
```

#### Task: Add System Report

```bash
# 1. Create Markdown file in data/reports/
# 2. Use clear filename: Purpose_YYYY-MM-DD.md
# 3. Include date, system state, findings
# 4. Reference relevant architecture/service docs

git add data/reports/New_Report_2025-11-20.md
git commit -m "Added system report: [brief summary]"
git push -u origin claude/claude-md-<session-id>
```

#### Task: Research Before Answering

**User asks:** "How do I configure Wazuh alerts for failed SSH logins?"

**AI Assistant should:**
1. Read `01_hawkinsops_high_level_architecture.md` for Wazuh setup
2. Read `30_services_matrix.md` for current Wazuh config
3. Check `40_sample_scripts_and_snippets.md` for existing Wazuh examples
4. Read `assumptions.md` for Wazuh Manager IP (192.168.50.10)
5. Provide answer referencing existing documentation
6. Suggest specific file paths for Wazuh config on Ubuntu server

#### Task: Suggest Infrastructure Changes

**User asks:** "Should I add a separate monitoring VLAN?"

**AI Assistant should:**
1. Read `assumptions.md` for current network design
2. Read `01_hawkinsops_high_level_architecture.md` for network architecture
3. Consider service dependencies in `30_services_matrix.md`
4. Evaluate impact on Wazuh agent connectivity
5. Check if change aligns with documented assumptions
6. Provide recommendation with specific VLAN ID, subnet, routing changes
7. Reference rebuild runbook sections that would need updates

### Response Quality Standards

**Good AI Response:**
```
Based on the architecture documented in 01_hawkinsops_high_level_architecture.md,
your Wazuh Manager is at 192.168.50.10 (as specified in assumptions.md).

To configure failed SSH login alerts:

1. SSH to Wazuh Manager: ssh raylee@192.168.50.10
2. Edit rules: sudo nano /var/ossec/etc/rules/local_rules.xml
3. Add the rule from 40_sample_scripts_and_snippets.md #25
4. Restart Wazuh: sudo systemctl restart wazuh-manager
5. Test: Generate failed SSH attempt from MINT-3 (192.168.50.102)
6. Verify alert in Wazuh dashboard

This follows the security pattern of "Audit Everything" documented in
your SOC design.
```

**Bad AI Response:**
```
Just add a Wazuh rule for SSH. Configure your server and it should work.
```

### Handling Uncertainty

**If you're unsure about infrastructure details:**
1. ✅ Explicitly state: "Let me check the architecture documentation first"
2. ✅ Read relevant files from blueprints/rebuild_pack/
3. ✅ Provide answer with file references
4. ❌ Don't guess IP addresses, hostnames, or configurations
5. ❌ Don't assume infrastructure beyond what's documented

**If documentation is unclear or missing:**
1. ✅ State: "The documentation doesn't specify X. Could you clarify?"
2. ✅ Suggest updating the documentation with the clarified information
3. ❌ Don't make assumptions that could break the environment

---

## 🔒 SECURITY CONSIDERATIONS

### Sensitive Data Handling

**Never commit to Git:**
- ❌ Passwords or password hashes
- ❌ API keys or tokens
- ❌ KeePassXC database files (`*.kdbx`)
- ❌ Private SSH keys
- ❌ Wazuh enrollment keys (if hardcoded)
- ❌ Financial data
- ❌ Personal identifiable information (PII)

**If user requests credential storage:**
1. ✅ Suggest using KeePassXC at `C:\HAWKINS_OPS\secure\hawkinsops.kdbx`
2. ✅ Recommend environment variables for scripts
3. ✅ Use placeholder text in documentation: `<password>`, `<api-key>`
4. ❌ Never write actual credentials to files in the repo

### Safe Script Recommendations

**When writing automation scripts:**
1. ✅ Include error handling (try/catch, set -e)
2. ✅ Validate inputs before execution
3. ✅ Log actions for audit trail
4. ✅ Use principle of least privilege
5. ✅ Include rollback procedures for risky operations
6. ❌ Never disable security controls (firewalls, logging, etc.)
7. ❌ Never run with unnecessary elevated privileges

### Infrastructure Safety

**Before suggesting changes that affect:**
- Network routing/firewall rules → Verify against pfSense config in architecture docs
- DNS configuration → Ensure AD DC (192.168.50.20) remains authoritative
- Wazuh agent configs → Verify manager IP (192.168.50.10) remains correct
- Domain settings → Ensure hawkinsops.local domain name preserved
- Service accounts → Recommend least privilege approach

---

## 📊 CURRENT PROJECT STATUS

**Phase:** Phase 2 Complete (as of 2025-11-03)
- ✅ Core infrastructure operational
- ✅ Wazuh SIEM deployed and monitoring
- ✅ Active Directory domain functional
- ✅ Automated backup workflow active
- ✅ Documentation complete and versioned

**Next Phase:** Phase 3 - Cloud/Mobile integration (planned)

**Maturity Level:**
- Documentation: Production-ready (v1.0)
- Automation: Basic (daily backups operational)
- Monitoring: Production (Wazuh SIEM 24/7)
- Testing: Manual health checks implemented

---

## 🎓 LEARNING CONTEXT

This repository represents a **career development project** for a SOC analyst position. When providing assistance:

**Career-Focused Perspective:**
- This is a resume builder and interview proof-of-capability
- Quality and professionalism matter (this will be reviewed by hiring managers)
- Documentation should demonstrate enterprise knowledge
- Scripts should show security best practices
- Architecture should reflect real-world SOC environments

**Educational Value:**
- Explain WHY, not just HOW when making recommendations
- Reference industry standards (MITRE ATT&CK, NIST, CIS Benchmarks)
- Connect changes to real-world SOC analyst responsibilities
- Highlight how features demonstrate job-relevant skills

**Example Enhanced Response:**
```
I recommend implementing this detection rule because:

1. MITRE ATT&CK Alignment: Detects T1078 (Valid Accounts)
2. SOC Analyst Skill: Demonstrates log analysis and correlation
3. Interview Talking Point: Shows understanding of authentication attacks
4. Real-World Value: This is a top-10 alert in enterprise SOCs

This enhancement to your lab directly supports your SOC analyst
career goal by showing expertise in threat detection.
```

---

## 📞 GETTING HELP

**If you encounter issues with:**
- Infrastructure assumptions → Read `blueprints/rebuild_pack/assumptions.md`
- Architecture questions → Read `blueprints/rebuild_pack/01_hawkinsops_high_level_architecture.md`
- Service problems → Check `blueprints/rebuild_pack/30_services_matrix.md` for health checks
- Rebuild procedures → Follow `blueprints/rebuild_pack/02_rebuild_master_runbook.md`
- Script examples → Reference `blueprints/rebuild_pack/40_sample_scripts_and_snippets.md`

**For AI assistants:**
- When uncertain, read the documentation first (blueprints/rebuild_pack/)
- Ask clarifying questions rather than making assumptions
- Reference specific file paths and line numbers when explaining
- Suggest documentation updates when gaps are found

---

## ✅ QUICK START CHECKLIST FOR AI ASSISTANTS

Before making any suggestions or changes:

- [ ] Read `assumptions.md` for critical infrastructure details
- [ ] Review `01_hawkinsops_high_level_architecture.md` for context
- [ ] Check `30_services_matrix.md` for current service state
- [ ] Understand current git branch (must start with `claude/`)
- [ ] Verify network ranges (192.168.50.0/24) and domain (hawkinsops.local)
- [ ] Review existing code patterns in `40_sample_scripts_and_snippets.md`
- [ ] Confirm no sensitive data will be committed
- [ ] Prepare clear commit messages
- [ ] Plan to push to correct branch with retry logic

**Your First Action:** When starting work on this repository, always begin by reading the blueprints/rebuild_pack/ documentation, especially `assumptions.md` and the architecture document.

---

## 📝 VERSION HISTORY

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-20 | Initial CLAUDE.md creation with comprehensive AI assistant guidelines |

---

**END OF CLAUDE.MD**

*This guide is maintained for AI assistants working with the HawkinsOps repository. Last updated: 2025-11-20*
