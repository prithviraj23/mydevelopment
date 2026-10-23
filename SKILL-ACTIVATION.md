# SKILL-ACTIVATION.md

How to activate the custom skills created for this workspace. All of them live at the **user level** (`~/.agents/skills/`), so they are available in every project, not just this one.

## How activation works

- **Automatically:** each skill's `description` is matched against the task — a Postgres, pytest, or marketing-science question triggers the matching skill without any command.
- **Explicitly:** type the slash command below (optionally followed by your instruction), e.g. `/postgresql-developer check why this query is slow`.
- **Discovery happens at session start.** Skills added or edited mid-session are picked up in a fresh ZCode session.

## Activation commands

| Skill | Command | What it covers (auto-triggers on) |
|---|---|---|
| Python Programmer | `/python-programmer` | Writing/refactoring Python, debugging tracebacks, venv & dependency management — tasks involving `.py` files, pip, uv |
| PostgreSQL Developer | `/postgresql-developer` | SQL authoring & optimization, schema design, migrations, psql usage, connection debugging, query performance |
| Data Scientist (Marketing Science) | `/data-scientist` | Media Mix Modelling (pymc-marketing default) and Customer Lifetime Value; ad spend, attribution, ROI, LTV/CAC, churn economics, RFM |
| Model Validation | `/model-validation` | Model evaluation and testing — splits, leakage, cross-validation, metrics, calibration, backtesting, and production drift monitoring/retraining triggers |
| Python Backend Tester | `/python-backend-tester` | Backend test suites — pytest design, fixtures, mocking boundaries, FastAPI/Flask test clients, PostgreSQL integration tests with isolation |
| Python Data Engineer | `/python-data-engineer` | Data pipelines for B2B SaaS on Azure — batch/streaming ELT, multi-tenant data models, event ingestion, usage metering, ADLS Gen2/Event Hubs/Functions/Key Vault |

## Combining skills

The skills cross-reference each other, and tasks often need two at once:

```
/python-programmer /python-backend-tester  add repository tests for the orders DAO
```

Typical pairings:

- **Python + Postgres:** writing a data-access layer — `/python-programmer` for the code, `/postgresql-developer` for the SQL and schema.
- **Data Scientist + Model Validation:** build an MMM, then validate its holdout honestly.
- **Backend Tester + Postgres:** integration tests with transaction-rollback isolation.

## Skill locations

```
~/.agents/skills/
├── python-programmer/SKILL.md
├── postgresql-developer/SKILL.md
├── data-scientist/            # SKILL.md + references/mmm.md, references/cltv.md
├── model-validation/SKILL.md
├── python-backend-tester/SKILL.md
└── python-data-engineer/          # SKILL.md + references/azure.md
```

Project-level skills can also live in `<project>/.zcode/skills/` or `<project>/.agents/skills/`; same-name skills there **override** the user-level ones during discovery.
