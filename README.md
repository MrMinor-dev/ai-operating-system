# AI Operating System

**The map of the system I run my business on: 25 skills, 36 workflows, 59 database tables, and the rules that hold them together.**

I have run my business on an AI system since August 2025. It reads its instructions from versioned skill files. It does its work through n8n workflows. It keeps its state in Postgres. It answers to a written contract that says what it may do alone and what needs my approval.

Each piece lives in its own repo, with the real files. This repo shows how the pieces connect.

## Start here

1. [ARCHITECTURE.md](ARCHITECTURE.md) has the system map and 2 walk-throughs of how work moves through it.
2. [CATALOG.md](CATALOG.md) lists every published skill, workflow, SQL file and framework, with links.
3. [GLOSSARY.md](GLOSSARY.md) explains the labels: CEO and COO, the authority tiers, the maturity levels.

## The 7 systems

| System | What it does | Repo |
|---|---|---|
| Governance | Decides what the agent may do. The contract, the 5 tiers, compliance checks. | [security-governance-framework](https://github.com/MrMinor-dev/security-governance-framework) |
| Data | Controls how the agent reaches the database. Row-level security, read-only queries, an allowlisted write path. | [database-security-framework](https://github.com/MrMinor-dev/database-security-framework) |
| Knowledge | Makes 781 business documents searchable by meaning. | [rag-knowledge-base](https://github.com/MrMinor-dev/rag-knowledge-base) |
| Comms | Slack in and out. Commands, alerts, the daily digest. | [n8n-development-framework](https://github.com/MrMinor-dev/n8n-development-framework) |
| Finance and email | Sorts email, logs expenses, watches the budget. | [back-office-automation](https://github.com/MrMinor-dev/back-office-automation) |
| Intel | Collects outside signals and analyzes them. | [n8n-development-framework](https://github.com/MrMinor-dev/n8n-development-framework) |
| Infra | Audits, error handling, remediation, site recovery. | [n8n-development-framework](https://github.com/MrMinor-dev/n8n-development-framework) |

The skills that tell the agent how to do all of this are in [ai-skills-framework](https://github.com/MrMinor-dev/ai-skills-framework). The working relationship between me and the agent is in [human-ai-coordination-framework](https://github.com/MrMinor-dev/human-ai-coordination-framework).

## The numbers

| Item | Value | Source |
|---|---|---|
| Workflows built | 40+ | n8n |
| Workflows published | 36 | [CATALOG.md](CATALOG.md) |
| Workflows active today | 26 | n8n |
| Skills published | 25, plus 1 retired | [CATALOG.md](CATALOG.md) |
| Database tables | 59, row-level security on all 59 | Supabase |
| Documents indexed | 781 | pgvector |
| Running since | August 2025 | |

## Frameworks

The [frameworks](frameworks/README.md) folder has 13 write-ups. Each covers one design problem: what broke, what I built, what I would tell a team starting on the same thing. Some describe parts that have since changed, and each says so.

## What's here

| Path | What it is |
|---|---|
| [ARCHITECTURE.md](ARCHITECTURE.md) | System map and walk-throughs. |
| [CATALOG.md](CATALOG.md) | Every published artifact, with links. |
| [GLOSSARY.md](GLOSSARY.md) | Terms and labels. |
| [frameworks/](frameworks/README.md) | 13 design write-ups and 3 worked examples. |
| [LICENSE](LICENSE) | MIT. |

## Built with

Claude and Claude Code, n8n, Supabase (Postgres and pgvector), Slack, Markdown skill files.

---

Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan) · [GitHub profile](https://github.com/MrMinor-dev)
