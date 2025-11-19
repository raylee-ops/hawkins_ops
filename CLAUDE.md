# CLAUDE.md - AI Assistant Guide for hawkins_ops

> **Last Updated:** 2025-11-19
> **Repository:** hawkins_ops
> **Type:** Personal Operations & Backup Automation System
> **Current Phase:** Phase 2 (Mirror Sync Setup)

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Repository Structure](#repository-structure)
3. [Key Conventions](#key-conventions)
4. [Development Workflows](#development-workflows)
5. [Working with Files](#working-with-files)
6. [Automation System](#automation-system)
7. [Important Constraints](#important-constraints)
8. [Common Tasks](#common-tasks)
9. [Troubleshooting](#troubleshooting)

---

## 🎯 Project Overview

### What is hawkins_ops?

**hawkins_ops** is a personal operations and backup automation system designed for:

- **Automated Daily Backups** - Local and cloud synchronization via Git
- **Compartmentalized Data Organization** - Structured storage for sensitive data, active work, and operational metadata
- **Version Control** - Git-based tracking of all changes with daily automated commits
- **Cloud Synchronization** - GitHub remote backup with scheduled pushes

### Current Status

- **Phase 1:** ✅ Complete - Infrastructure setup
- **Phase 2:** ✅ Complete - Mirror sync automation operational
- **Phase 3:** 🔄 Planned - Apple/Cloud agent integration

### System Context

- **Host:** Windows machine (WIN-E910N6HGLH9)
- **Primary User:** Raylee (raylee@hawkinsops.com)
- **Automation:** Daily sync at 23:00 UTC via Windows Task Scheduler
- **PowerShell Version:** 7.5.4
- **Git Version:** 2.51.2.windows.1

---

## 📁 Repository Structure

### Four-Pillar Organization Model

```
hawkins_ops/
├── data/                  # Operational metadata and logs
│   ├── archives/         # Historical/archived data
│   ├── logs/             # Automation execution logs (ROBOCOPY format)
│   ├── notes/            # Working notes and documentation
│   └── reports/          # Generated reports and analysis
│
├── vault/                # Sensitive/secure data storage
│   ├── finances/         # Financial records
│   ├── personal/         # Personal information
│   └── projects/         # Project-specific secure data
│
├── workspace/            # Active working directories
│   ├── active/           # Current work items
│   │   └── labs/         # Experimental/lab work
│   ├── reference/        # Reference materials
│   └── temp/             # Temporary files
│
└── system/               # System infrastructure
    ├── config/           # Configuration files
    ├── scripts/          # Automation scripts
    │   └── autosync.ps1  # Primary automation script
    └── templates/        # Reusable templates
```

### Directory Purposes

| Directory | Purpose | Current State |
|-----------|---------|---------------|
| `data/logs/` | ROBOCOPY execution logs (15 files) | Active |
| `data/reports/` | Status reports (Phase_2_Report.md) | Active |
| `data/notes/` | Working notes placeholder | Empty (ready) |
| `data/archives/` | Historical data storage | Empty (ready) |
| `vault/finances/` | Financial records | Empty (ready) |
| `vault/personal/` | Personal information | Empty (ready) |
| `vault/projects/` | Secure project data | Empty (ready) |
| `workspace/active/` | Current work area | Empty (ready) |
| `workspace/reference/` | Reference materials | Empty (ready) |
| `workspace/temp/` | Temporary files | Empty (ready) |
| `system/config/` | Configuration files | Empty (ready) |
| `system/scripts/` | Automation scripts | 1 file (autosync.ps1) |
| `system/templates/` | Reusable templates | Empty (ready) |

### Important Files

- **`system/scripts/autosync.ps1`** - Primary automation script (mirrors files, commits, pushes)
- **`data/reports/Phase_2_Report.md`** - Phase 2 status and system documentation
- **`data/logs/mirror_*.log`** - Daily ROBOCOPY execution logs
- **`.keep` files** - Maintain directory structure in Git (17 total)

---

## 🔑 Key Conventions

### Naming Conventions

| Element | Pattern | Example |
|---------|---------|---------|
| **Log Files** | `mirror_YYYYMMdd_HHmmss.log` | `mirror_20251117_230004.log` |
| **Git Commits** | `Auto-sync: YYYY-MM-DD HH:mm:ss` | `Auto-sync: 2025-11-17 23:00:04` |
| **Directories** | Lowercase, functional names | `vault`, `workspace`, `data` |
| **Subdirectories** | Single-word, categorical | `finances`, `personal`, `projects` |

### Architectural Principles

1. **Separation of Concerns**
   - `vault/` = Confidential/sensitive data
   - `workspace/` = Active working areas
   - `data/` = Logs, notes, and reports (operational metadata)
   - `system/` = Infrastructure and automation

2. **Immutable Structure**
   - Directory tree maintained via `.keep` files
   - Structure persists even when directories are empty
   - Enables future content without structural changes

3. **Automated Synchronization**
   - Single daily commit at 23:00 UTC
   - Local mirror backup + GitHub push
   - Consistent, predictable automation

4. **Version Control Everything**
   - All changes tracked in Git
   - Daily automated commits preserve history
   - Cloud backup via GitHub

---

## ⚙️ Development Workflows

### Understanding the Automation Cycle

The system runs on a **daily automation schedule**:

```
23:00 UTC Daily
    ↓
1. ROBOCOPY Mirror
   C:\HAWKINS_OPS → D:\Backups\HAWKINS_OPS
   (Currently failing - D: drive not available)
    ↓
2. Git Stage All Changes
   git add .
    ↓
3. Git Commit
   Format: "Auto-sync: YYYY-MM-DD HH:mm:ss"
    ↓
4. Git Push to GitHub
   Remote: raylee-ops/hawkins_ops
    ↓
5. Log Results
   Save to: data/logs/mirror_YYYYMMdd_HHmmss.log
```

### Making Changes to This Repository

When working with this repository, follow these workflows:

#### 1. Adding New Content

```bash
# Add files to appropriate directory based on content type:
# - Sensitive data → vault/
# - Active work → workspace/active/
# - Notes/docs → data/notes/
# - Reports → data/reports/
# - System configs → system/config/
# - Scripts → system/scripts/
# - Templates → system/templates/

# Example: Adding a new note
echo "Content" > data/notes/new_note.txt

# Git will automatically track and commit at next sync (23:00 UTC)
# OR commit manually:
git add .
git commit -m "Add: new_note.txt with [description]"
git push origin main
```

#### 2. Modifying Automation Scripts

```bash
# Edit the autosync script
vim system/scripts/autosync.ps1

# Test changes locally before committing
pwsh system/scripts/autosync.ps1

# Commit with descriptive message
git add system/scripts/autosync.ps1
git commit -m "Update: autosync.ps1 - [describe changes]"
git push origin main
```

#### 3. Adding New Reports

```bash
# Reports go in data/reports/
# Use descriptive names: Phase_N_Report.md, Analysis_YYYYMMDD.md

# Create new report
vim data/reports/Analysis_20251119.md

# Commit
git add data/reports/
git commit -m "Add: Analysis report for 2025-11-19"
git push origin main
```

#### 4. Managing Vault Content

```bash
# Vault contains sensitive data - be cautious
# Ensure .gitignore properly excludes sensitive files if needed

# Add to appropriate vault subdirectory
# - vault/finances/ → Financial records
# - vault/personal/ → Personal information
# - vault/projects/ → Project-specific secure data
```

### Git Commit Message Format

Follow these conventions for manual commits:

- **Add:** `Add: [filename] - [brief description]`
- **Update:** `Update: [filename] - [what changed]`
- **Fix:** `Fix: [issue description]`
- **Remove:** `Remove: [filename] - [reason]`
- **Refactor:** `Refactor: [component] - [what improved]`

**Automated commits** use: `Auto-sync: YYYY-MM-DD HH:mm:ss`

---

## 📝 Working with Files

### File Type Guidelines

| File Type | Location | Purpose |
|-----------|----------|---------|
| **PowerShell Scripts** | `system/scripts/` | Automation and tooling |
| **Markdown Docs** | `data/reports/` or `data/notes/` | Documentation and notes |
| **Configuration Files** | `system/config/` | System configuration |
| **Templates** | `system/templates/` | Reusable file templates |
| **Log Files** | `data/logs/` | Automation execution logs |
| **Archive Data** | `data/archives/` | Historical/aged data |
| **Financial Records** | `vault/finances/` | Financial documents |
| **Personal Data** | `vault/personal/` | Personal information |
| **Project Data** | `vault/projects/` | Project-specific secure files |
| **Active Work** | `workspace/active/` | Current work items |
| **Reference Materials** | `workspace/reference/` | Reference documents |
| **Temporary Files** | `workspace/temp/` | Temporary/disposable files |

### Reading Existing Files

Before modifying any file, **always read it first**:

```bash
# Read the autosync script
cat system/scripts/autosync.ps1

# Read the Phase 2 report
cat data/reports/Phase_2_Report.md

# Check recent logs
cat data/logs/mirror_20251117_230004.log
```

### Creating New Files

**IMPORTANT:** Only create files when necessary. Always prefer:
1. **Editing existing files** over creating new ones
2. **Using existing directories** (don't create new top-level directories)
3. **Following naming conventions** for consistency

---

## 🤖 Automation System

### Primary Script: autosync.ps1

**Location:** `system/scripts/autosync.ps1`

**Operations:**
1. **Local Mirror Backup** (ROBOCOPY)
   - Source: `C:\HAWKINS_OPS`
   - Destination: `D:\Backups\HAWKINS_OPS`
   - Options: `/MIR` (mirror), `/R:1 /W:1` (minimal retries)
   - Current Status: ⚠️ **Failing** (D: drive not available)

2. **Git Commit**
   - Stages all changes: `git add .`
   - Commits with timestamp: `Auto-sync: YYYY-MM-DD HH:mm:ss`

3. **Git Push**
   - Pushes to: `origin main`
   - Remote: GitHub (raylee-ops/hawkins_ops)

4. **Logging**
   - Output saved to: `data/logs/mirror_YYYYMMdd_HHmmss.log`
   - Format: Standard ROBOCOPY output (20 lines per log)

### Execution Schedule

**Windows Task Scheduler:**
- **Task Name:** `HawkinsOps_AutoSync`
- **Schedule:** Daily at 23:00 UTC (11:00 PM)
- **User:** Raylee
- **Status:** ✅ Operational (running since Nov 2, 2025)

### Known Issues

⚠️ **Backup Drive Not Available**
- ROBOCOPY fails: `D:\` path not found
- Issue persists since November 2, 2025
- Git operations continue successfully
- **Impact:** Local mirror backup not functioning, GitHub backup operational

---

## ⚠️ Important Constraints

### DO NOT:

1. **Delete `.keep` files** - They maintain the directory structure in Git
2. **Create new top-level directories** - Use the existing four-pillar structure
3. **Modify log files in `data/logs/`** - These are generated by automation
4. **Change the directory structure** - It's intentionally designed for compartmentalization
5. **Skip reading files before editing** - Always read existing content first
6. **Create unnecessary documentation** - Only create docs when explicitly needed
7. **Commit secrets/credentials** - Be cautious with vault content

### DO:

1. **Follow naming conventions** - Consistency is critical
2. **Use appropriate directories** - Place files in their designated locations
3. **Read before writing** - Understand existing content
4. **Test scripts before committing** - Especially for `autosync.ps1`
5. **Write clear commit messages** - Describe what and why
6. **Preserve the automation cycle** - Don't break the daily sync
7. **Respect the security model** - Vault is for sensitive data

---

## 🔧 Common Tasks

### Task 1: Add a New Automation Script

```bash
# 1. Create script in system/scripts/
vim system/scripts/new_automation.ps1

# 2. Make it executable (if needed)
chmod +x system/scripts/new_automation.ps1

# 3. Test it
pwsh system/scripts/new_automation.ps1

# 4. Commit
git add system/scripts/new_automation.ps1
git commit -m "Add: new_automation.ps1 - [describe purpose]"
git push origin main
```

### Task 2: Create a New Report

```bash
# 1. Create report in data/reports/
vim data/reports/New_Report_20251119.md

# 2. Follow markdown format
# Include: Date, Purpose, Findings, Next Steps

# 3. Commit
git add data/reports/New_Report_20251119.md
git commit -m "Add: New report for 2025-11-19"
git push origin main
```

### Task 3: Update the Autosync Script

```bash
# 1. Read current script
cat system/scripts/autosync.ps1

# 2. Make changes
vim system/scripts/autosync.ps1

# 3. Test locally
pwsh system/scripts/autosync.ps1

# 4. Review output and logs
cat data/logs/mirror_*.log | tail -30

# 5. If successful, commit
git add system/scripts/autosync.ps1
git commit -m "Update: autosync.ps1 - [describe changes]"
git push origin main
```

### Task 4: Add Configuration Files

```bash
# 1. Create config in system/config/
vim system/config/app_config.json

# 2. Validate format (JSON, YAML, etc.)
# Use appropriate validator

# 3. Commit
git add system/config/app_config.json
git commit -m "Add: app_config.json for [purpose]"
git push origin main
```

### Task 5: Archive Old Data

```bash
# 1. Move old files to archives
mv data/notes/old_note.txt data/archives/

# 2. Commit
git add data/notes/ data/archives/
git commit -m "Archive: old_note.txt (completed 2025-11-19)"
git push origin main
```

---

## 🔍 Troubleshooting

### Issue: Autosync Not Running

**Symptoms:**
- No new commits after 23:00 UTC
- No new log files in `data/logs/`

**Diagnosis:**
```powershell
# Check Task Scheduler status (Windows)
Get-ScheduledTask -TaskName "HawkinsOps_AutoSync"

# Check last run time
Get-ScheduledTaskInfo -TaskName "HawkinsOps_AutoSync"
```

**Resolution:**
1. Verify Task Scheduler is enabled
2. Check autosync.ps1 for syntax errors
3. Run script manually to test: `pwsh system/scripts/autosync.ps1`
4. Review latest log in `data/logs/`

---

### Issue: ROBOCOPY Backup Failing

**Symptoms:**
- Logs show "ERROR 3 (0x00000003)" or path not found
- D: drive destination unreachable

**Diagnosis:**
```bash
# Check recent logs
cat data/logs/mirror_20251117_230004.log

# Look for ERROR messages in ROBOCOPY output
```

**Current Status:**
⚠️ This is a **known issue** since November 2, 2025
- **Cause:** D: drive not available/mounted
- **Impact:** Local mirror backup not functioning
- **Workaround:** GitHub backup still operational

**Resolution:**
1. **Windows System:** Verify D: drive is mounted and accessible
2. **Update Script:** If drive letter changed, update `autosync.ps1` destination path
3. **Alternative:** Consider cloud-only backup if local drive not needed

---

### Issue: Git Push Failing

**Symptoms:**
- Commits succeed but push fails
- Authentication errors
- Network errors

**Diagnosis:**
```bash
# Check remote configuration
git remote -v

# Test connection
git fetch origin

# Check authentication
git config --list | grep user
```

**Resolution:**
1. Verify GitHub credentials/SSH keys
2. Check network connectivity
3. Ensure remote URL is correct
4. If using proxy, verify proxy configuration

---

### Issue: Directory Structure Changed

**Symptoms:**
- Missing `.keep` files
- New unexpected top-level directories

**Diagnosis:**
```bash
# List all .keep files (should be 17)
find . -name ".keep" | wc -l

# Check top-level directories (should be 4: data, vault, workspace, system)
ls -d */
```

**Resolution:**
1. **Restore `.keep` files** if deleted
2. **Remove unauthorized top-level directories** - move content to appropriate location
3. **Commit fixes** immediately to restore structure

---

## 📚 Additional Resources

### Documentation Files

- **Phase 2 Report:** `data/reports/Phase_2_Report.md`
  - System host information
  - Configuration details
  - Automation status
  - Known issues
  - Future roadmap (Phase 3)

### Execution Logs

- **Location:** `data/logs/`
- **Format:** `mirror_YYYYMMdd_HHmmss.log`
- **Count:** 15 logs (November 2-17, 2025)
- **Content:** ROBOCOPY output (20 lines per log)

### Git History

- **Baseline Commit:** `80ee0e2` - Phase 2 initial mirror setup
- **Latest Commit:** `2a97dcc` - Auto-sync: 2025-11-17 23:00:04
- **Pattern:** Daily automated commits at 23:00 UTC
- **Total Commits:** 16+ (Nov 2-17, 2025)

---

## 🎓 Quick Reference for AI Assistants

### When Working with This Repository:

1. **Understand the Purpose:** Personal operations/backup system, NOT a software project
2. **Respect the Structure:** Four-pillar organization (data/vault/workspace/system)
3. **Check Existing Files First:** Always read before editing
4. **Use Appropriate Directories:** Match content type to directory purpose
5. **Follow Naming Conventions:** Consistent patterns for logs, commits, files
6. **Test Before Committing:** Especially for automation scripts
7. **Preserve `.keep` Files:** They maintain Git directory structure
8. **Be Security-Aware:** Vault contains sensitive data
9. **Document Changes:** Clear commit messages and reports when needed
10. **Monitor Automation:** Check logs for execution status

### Most Common Operations:

- **Add new automation:** `system/scripts/`
- **Create reports:** `data/reports/`
- **Add notes:** `data/notes/`
- **Store configs:** `system/config/`
- **Archive data:** `data/archives/`
- **Check logs:** `data/logs/`

### Key Files to Know:

- `system/scripts/autosync.ps1` - **The automation engine**
- `data/reports/Phase_2_Report.md` - **System documentation**
- `data/logs/mirror_*.log` - **Execution history**

---

## 📝 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-19 | Initial CLAUDE.md creation - comprehensive repository documentation |

---

**For questions or issues, refer to:**
- Phase 2 Report: `data/reports/Phase_2_Report.md`
- Execution Logs: `data/logs/`
- Git History: `git log --oneline`

**System Owner:** Raylee (raylee@hawkinsops.com)
**Repository:** https://github.com/raylee-ops/hawkins_ops
