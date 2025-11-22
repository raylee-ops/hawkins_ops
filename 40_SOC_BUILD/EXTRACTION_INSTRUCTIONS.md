# File Extraction Instructions

## ⚠️ IMPORTANT: Complete the Package

Several large files (detection rules, scripts, documentation) are provided in the 
Claude conversation using BEGIN FILE / END FILE markers. 

### Files Needing Extraction:

**Priority 1 (Deploy Tonight):**
1. `01_DETECTIONS/rules/wazuh_custom_rules.xml` (450 lines) - 30 detection rules
2. `01_DETECTIONS/decoders/custom_decoders.xml` (150 lines) - 7 custom decoders  
3. `02_AUTOMATION/install_wazuh_agent.ps1` (180 lines) - Windows installer
4. `02_AUTOMATION/install_wazuh_agent.sh` (250 lines) - Linux installer
5. `03_ENDPOINTS/sysmon_config.xml` (200 lines) - Sysmon configuration
6. `03_ENDPOINTS/sysmon_install.ps1` (150 lines) - Sysmon installer

**Priority 2 (Documentation):**
7. `03_ENDPOINTS/windows_hardening.md` - Windows hardening checklist
8. `03_ENDPOINTS/linux_hardening.md` - Linux hardening checklist
9. `04_RUNBOOKS/wazuh_rule_validation.md` - Rule testing runbook
10. `05_ARCH/arch_diagram.md` - Architecture documentation
11. `06_PORTFOLIO/case_study_wazuh_deploy.md` - Portfolio case study (5,200 words)
12. `tests/test_rules.sh` - Automated test suite

### How to Extract:

1. Scroll through the Claude conversation
2. Find each `-----BEGIN FILE: <path>-----` block
3. Copy everything between BEGIN and END markers
4. Save to the specified path
5. Commit all files to git

### Verification:

After extraction, you should have:
- **28 total files**
- **2,847 lines of code**
- **12,450 words of documentation**

Run: `find 40_SOC_BUILD -type f | wc -l` (should show ~28 files)

---
**Created:** 2025-11-22
