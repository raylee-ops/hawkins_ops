# HawkinsOps SOC V1 - Quick Deployment Guide

**Time Required:** 60-90 minutes for full deployment
**Prerequisites:** Wazuh Manager already installed, Windows 11 + Linux Mint endpoints accessible

---

## Minimum POC Deployment (15 Minutes)

### On Wazuh Manager (Linux):

```bash
# 1. Copy detection rules (2 minutes)
sudo cp 40_SOC_BUILD/01_DETECTIONS/rules/wazuh_custom_rules.xml /var/ossec/etc/rules/
sudo cp 40_SOC_BUILD/01_DETECTIONS/decoders/custom_decoders.xml /var/ossec/etc/decoders/
sudo chown ossec:ossec /var/ossec/etc/rules/wazuh_custom_rules.xml
sudo chown ossec:ossec /var/ossec/etc/decoders/custom_decoders.xml

# 2. Test syntax and restart Wazuh (3 minutes)
sudo /var/ossec/bin/ossec-logtest -t
sudo systemctl restart wazuh-manager
sudo systemctl status wazuh-manager

# 3. Verify rules loaded (1 minute)
sudo grep "Rule id: '100" /var/ossec/logs/ossec.log
```

### On Windows 11 Endpoint (PowerShell as Administrator):

```powershell
# 4. Install Wazuh agent (5 minutes)
cd C:\path\to\40_SOC_BUILD\02_AUTOMATION
.\install_wazuh_agent.ps1 -ManagerIP "192.168.1.10" -AgentName "WIN11-HAWKINS"

# 5. Install Sysmon (3 minutes)
cd C:\path\to\40_SOC_BUILD\03_ENDPOINTS
.\sysmon_install.ps1

# 6. Enable PowerShell logging (1 minute)
New-Item -Path "HKLM:\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name "EnableScriptBlockLogging" -Value 1
```

### On Linux Mint Endpoint (Bash):

```bash
# 7. Install Wazuh agent (5 minutes)
cd /path/to/40_SOC_BUILD/02_AUTOMATION
sudo bash install_wazuh_agent.sh 192.168.1.10 LINUX-HAWKINS
```

---

## Validation (5 Minutes)

### Check Agent Connectivity:

```bash
# On Wazuh Manager
sudo /var/ossec/bin/agent_control -l

# Expected output: Both agents shown as "Active"
```

### Generate Test Alert:

```powershell
# On Windows 11 (PowerShell)
powershell.exe -ExecutionPolicy Bypass -enc QwBvAG0AbQBhAG4AZAA=
```

```bash
# On Wazuh Manager - check for alert
sudo tail -f /var/ossec/logs/alerts/alerts.log | grep "Rule: 100102"
```

**Expected:** Rule 100102 (Suspicious PowerShell) alert appears within 1-2 minutes

---

**Deployment Confidence:** 90% - Tested in isolated lab environment. Minor tuning expected based on your specific endpoint configurations.

**Last Updated:** 2025-11-22
