# WINDOWS BUILD PROMPTS

## Machine: Windows Powerhouse
## Run these in exact order (1-9)

---

## PROMPT 1 — Create Tracker Folder + Empty Files

```
You are CLAUDE CODE.

TASK:
Create this structure under PRIMARY_OS/tools/progress:

- progress.db   (empty SQLite database)
- progress.py   (empty Python file)
- readme.md     (placeholder text)

Do NOT add logic yet.
Do NOT touch other directories.
Show me the created paths after.
```

---

## PROMPT 2 — Create SQLite Schema Inside DB

```
TASK:
Initialize progress.db with this schema:

CREATE TABLE IF NOT EXISTS daily_logs(
  date TEXT PRIMARY KEY,
  hawkinsops_hours REAL,
  security_hours REAL,
  labs_completed INTEGER,
  scripts_touched INTEGER,
  apps_sent INTEGER,
  conversations INTEGER,
  life_admin INTEGER,
  health_score INTEGER,
  text_log TEXT,
  streak INTEGER,
  momentum REAL
);

Only create schema. No CLI logic yet.
```

---

## PROMPT 3 — Add Basic CLI Skeleton (argparse)

```
TASK:
Append to progress.py:

Create argparse CLI with two subcommands:
- log
- summary

For now:
log → print("log mode")
summary → print("summary mode")

Do not add database logic yet.
```

---

## PROMPT 4 — Implement log_today() With Only 3 Inputs

```
TASK:
Implement log_today() in progress.py:

For today's date, prompt for:
- hawkinsops_hours (float)
- security_hours (float)
- text_log (string)

Insert/update row in daily_logs.

Do NOT implement streak or momentum yet.
Bind this to the "log" subcommand.
```

---

## PROMPT 5 — Add Streak + Momentum Calculation

```
TASK:
Upgrade log_today():

- streak:
  count consecutive days where (hawkinsops_hours + security_hours) > 0

- momentum:
  simple score = (hawkinsops_hours + security_hours) / 2

Write both values into today's row.
```

---

## PROMPT 6 — Implement Summary Mode

```
TASK:
Implement summary mode in progress.py:

- Fetch last 7 entries from daily_logs ORDER BY date DESC
- Print: date, hawkinsops_hours, security_hours, momentum
```

---

## PROMPT 7 — Begin Documentation Pack: Inventory Scan

```
You are CLAUDE CODE.

TASK:
Scan PRIMARY_OS/HAWKINS_OPS and produce a clean inventory of:
- folders
- major files
- scripts
- labs
- configs

Do NOT write or move anything yet. Inventory only.
```

---

## PROMPT 8 — Create docs_pack Folder + Empty MD Files

```
TASK:
Create PRIMARY_OS/HAWKINS_OPS/docs_pack with:

- overview.md
- architecture.md
- labs_index.md
- scripts_index.md
- resume_bullets.md

Put "PLACEHOLDER" in each file.
Do NOT fill content yet.
```

---

## PROMPT 9 — Fill Each Documentation File

```
TASK:
Populate each docs_pack markdown file:

overview.md → summary of HawkinsOps purpose, machines, goals
architecture.md → network flow, components, data paths
labs_index.md → list of labs + purpose
scripts_index.md → list of automation scripts + purpose
resume_bullets.md → high-impact resume bullets based on findings

Use clear headings and short paragraphs.
Do not modify user files outside docs_pack.
```

---

## CHECKPOINT

After running all 9 prompts, you should have:

✔ `PRIMARY_OS/tools/progress/progress.db`
✔ `PRIMARY_OS/tools/progress/progress.py`
✔ `PRIMARY_OS/HAWKINS_OPS/docs_pack/` (5 markdown files)

**Next:** Switch to Linux Mint and run `raylee_prompts_linux.md`
