# Catalog

Every published skill, workflow, SQL file and framework, with links. Counts come from the folders as published.

| Item | Count |
|---|---|
| Skills | 25 (plus 1 retired) |
| Workflows | 36 |
| Frameworks | 13 |

## Skills

### Sessions

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [session-end-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/session-end-skill/SKILL.md) | 1.23 | Chat assistant | Closes a session: records decisions, updates the state document, flags unfinished work. |
| [session-start-day-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/session-start-day-skill/SKILL.md) | - | Chat assistant | Gives the daily briefing on the first session of the day. |
| [session-startup-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/session-startup-skill/SKILL.md) | - | Chat assistant | Reloads state for a mid-day session and routes to a focus area. |

### Knowledge

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [doc-management-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/doc-management-skill/SKILL.md) | 2.23 | Chat assistant | Creates and edits documents to a fixed standard: frontmatter, source-of-truth status, registry entry. |
| [quarterly-doc-audit-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/quarterly-doc-audit-skill/SKILL.md) | 2.5 | Chat assistant | Runs the quarterly documentation audit in phases. |
| [semantic-index-update-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/semantic-index-update-skill/SKILL.md) | - | Chat assistant | Updates the search index after files change. |
| [semantic-reindex](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/semantic-reindex/SKILL.md) | - | Coding agent | Incrementally updates the search index for changed files. |
| [semantic-search](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/semantic-search/SKILL.md) | - | Coding agent | Searches the knowledge base for context (Claude Code version). |
| [semantic-search-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/semantic-search-skill/SKILL.md) | - | Chat assistant | Searches the knowledge base before any large file is loaded. |
| [wikify-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/wikify-skill/SKILL.md) | 1.0 | Chat assistant | Turns raw assets into wiki pages in 4 steps: extract, route, generate, validate. |

### Workflow engineering

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [n8n-diagnose](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/n8n-diagnose/SKILL.md) | - | Coding agent | Diagnoses failing n8n workflows in 4 phases: evidence, diagnose, fix, verify. |
| [n8n-workflow-audit](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/n8n-workflow-audit/SKILL.md) | - | Coding agent | Scores an n8n workflow against the 65-point checklist. |
| [n8n-workflow-build](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/n8n-workflow-build/SKILL.md) | - | Coding agent | Builds or modifies n8n workflows from a spec through the REST API. |
| [workflow-build-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/workflow-build-skill/SKILL.md) | 2.0 | Chat assistant | Builds n8n workflows from a spec, with the audit as a gate. |
| [workflow-reactivation-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/workflow-reactivation-skill/SKILL.md) | 1.8 | Chat assistant | Checklist for moving a workflow out of production or back into it. |

### Data

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [database-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/database-skill/SKILL.md) | - | Chat assistant | Runs database operations safely: checks the live schema first, then works through the guarded services. |

### Oversight

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [archive](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/archive/SKILL.md) | - | Coding agent | Moves finished artifacts to a cold archive under self-locating names. |
| [cc-audit-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/cc-audit-skill/SKILL.md) | 1.0 | Chat assistant | Audits a finished Claude Code run and classifies it clean, issue or storm. |
| [post-mortem-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/post-mortem-skill/SKILL.md) | 1.1 | Chat assistant | Writes incident post-mortems and closes the learning loop. |
| [process-feedback](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/process-feedback/SKILL.md) | 1.9 | Coding agent | Turns a Claude Code feedback file into proposed environment updates. It proposes, and a person approves. |

### Delegation and authoring

| Skill | Version | Runs in | What it does |
|---|---|---|---|
| [cc-prompt-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/cc-prompt-skill/SKILL.md) | 1.38 | Chat assistant | Writes the task prompts that delegate work to Claude Code, and processes the feedback that comes back. |
| [github-update-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/github-update-skill/SKILL.md) | - | Coding agent | Drafts GitHub READMEs and the prompts that push them. |
| [pdf-creation-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/pdf-creation-skill/SKILL.md) | 1.0 | Chat assistant | Builds PDF documents. |
| [pptx-creation-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/pptx-creation-skill/SKILL.md) | 1.0 | Chat assistant | Builds presentation decks. |
| [skill-creator-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/skill-creator-skill/SKILL.md) | 3.8 | Chat assistant | Creates, validates and packages new skills. |

### Retired

| Skill | Version | What it was |
|---|---|---|
| [workflow-audit-skill](https://github.com/MrMinor-dev/ai-skills-framework/blob/main/skills/_retired/workflow-audit-skill/SKILL.md) | 2.1 | The original 60-point workflow audit. Replaced by n8n-workflow-audit. |

## Workflows

Levels: L1 logs success, L2 also handles errors, L3 also calls the remediation trigger. See the [glossary](GLOSSARY.md).

### Governance (2)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS-Compliance-Policy-Monitor](https://github.com/MrMinor-dev/security-governance-framework/blob/main/workflows/governance/aos-compliance-policy-monitor.json) | Daily watch on FTC and platform policy feeds. Stores new alerts. Not in production. *(not in production)* | schedule, feeds | - | security-governance-framework |
| [AOS-Compliance-Spot-Audit](https://github.com/MrMinor-dev/security-governance-framework/blob/main/workflows/governance/aos-compliance-spot-audit.json) | Daily random sample of generated content, checked for disclosure and affiliate-tag rules. Critical failures alert Slack. Built for a content operation that has ended. Not in production. *(not in production)* | schedule, webhook | - | security-governance-framework |

### Data (2)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Database - Safe DB Write](https://github.com/MrMinor-dev/database-security-framework/blob/main/workflows/data/aos-database-safe-db-write.json) | Allowlisted write service. Validates INSERT, UPDATE and DELETE against a table and column allowlist. Being rebuilt (see the note in database-security-framework). | webhook | L2 | database-security-framework |
| [AOS - Database - Safe SQL Query](https://github.com/MrMinor-dev/database-security-framework/blob/main/workflows/data/aos-database-safe-sql-query.json) | Read-only SQL service over a webhook. Blocks writes and DDL, returns at most 50 rows. | webhook | L2 | database-security-framework |

### Knowledge (7)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Intel Asset-Wikifier](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/knowledge/aos-intel-asset-wikifier.json) | Extracts signals from a business asset with Claude, routes them to wiki pages, and writes or updates those pages. | webhook | L2 | n8n-development-framework |
| [HAIOS - Database - Semantic Search](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/workflows/knowledge/haios-database-semantic-search.json) | Embeds a question and returns the closest document chunks from pgvector. | webhook | L2 | rag-knowledge-base |
| [HAIOS - Database - Semantic Search Transcripts](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/workflows/knowledge/haios-database-semantic-search-transcripts.json) | Same search as the docs workflow, aimed at session-transcript embeddings. Not in production. *(not in production)* | webhook | L2 | rag-knowledge-base |
| [HAIOS-Intel-Wiki-Explore](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/knowledge/haios-intel-wiki-explore.json) | Picks recent analyses and sends each one to the wikifier. | schedule, webhook | - | n8n-development-framework |
| [HAIOS-Intel-Wiki-Lint](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/knowledge/haios-intel-wiki-lint.json) | Checks wiki pages with Claude and records new issues. | schedule, webhook | - | n8n-development-framework |
| [HAIOS-Intel-Wiki-Lint-Triage](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/knowledge/haios-intel-wiki-lint-triage.json) | Classifies open wiki issues with Claude Haiku, dismisses false positives, and writes fix instructions for the rest. | schedule, webhook | - | n8n-development-framework |
| [HAIOS-Intel-Wiki-Query](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/knowledge/haios-intel-wiki-query.json) | Answers a question from the wiki pages with Claude. | webhook | - | n8n-development-framework |

### Comms (5)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [HAIOS - Comms - Daily Digest](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-daily-digest.json) | Compiles overnight messages, expenses, health checks, intel, pending remediations and wiki issues into one Slack digest. | schedule | L2 | n8n-development-framework |
| [HAIOS - Comms - Slack Inbound (Control Plane)](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-slack-inbound-control-plane.json) | Receives Slack commands (kill, resume, status, help), ignores the bot's own messages, and routes each command. | Slack | L2 | n8n-development-framework |
| [HAIOS - Comms - Slack Outbound](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-slack-outbound.json) | Shared send service. Any workflow calls it to post a Slack message. | webhook | L2 | n8n-development-framework |
| [HAIOS - Comms - Weekly Report](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-weekly-report.json) | Monday summary of landscape intelligence and win/loss. | schedule | L2 | n8n-development-framework |
| [Utility - Gmail Query](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/utility-gmail-query.json) | Lists Gmail labels on demand for other workflows. | manual/chat | L1 | n8n-development-framework |

### Finance (3)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Finance - Budget Monitor](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-budget-monitor.json) | Compares month-to-date expenses with the budget and alerts on breaches. Checks alert history to avoid duplicates. | schedule, webhook | L2 | back-office-automation |
| [AOS - Finance - Expense Entry](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-expense-entry.json) | Validates an expense, maps it to a tax category, rejects bad input, and inserts it. | webhook | L2 | back-office-automation |
| [AOS - Finance - Invoice Handler](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-invoice-handler.json) | Reads flagged financial emails each morning, extracts vendor, amount and dates, and writes expense rows. | schedule | L2 | back-office-automation |

### Email (3)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Email - Email Router](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/email/aos-email-email-router.json) | Classifies each incoming email with sender rules, labels it, and archives or keeps it. Includes a backfill path. | email, webhook | L2 | back-office-automation |
| [AOS - Email - Inbox Cleanup](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/email/aos-email-inbox-cleanup.json) | Manual cleanup of four Gmail label buckets (quarantine, and platform, vendor and action mail older than 60 days). Runs in dry-run mode by default. *(not in production)* | manual/chat | L2 | back-office-automation |
| [AOS - Email- Quarantine Manager](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/email/aos-email-quarantine-manager.json) | Sends a daily digest of quarantined emails to Slack and archives the expired ones. | schedule | L2 | back-office-automation |

### Intel (6)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Intel - Email Collector](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/aos-intel-email-collector.json) | Collects signals from platform and vendor emails each night. | schedule | L2 | n8n-development-framework |
| [AOS - Intel - Stack Updates Collector](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/aos-intel-stack-updates-collector.json) | Collects release news from the tools the system runs on, nightly. | schedule, feeds | L2 | n8n-development-framework |
| [AOS-Intel-n8n-Metrics-Collector](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/aos-intel-n8n-metrics-collector.json) | Every 6 hours, aggregates execution metrics from n8n and stores them. | schedule, webhook | - | n8n-development-framework |
| [HAIOS - Intel - 3P Collector](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/haios-intel-3p-collector.json) | Collects third-party signals from social and blog sources into the intel tables. | schedule | L2 | n8n-development-framework |
| [HAIOS - Intel - Analyzer](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/haios-intel-analyzer.json) | Analyzes collected signals with Claude and semantic search, classifies them, and writes the analyses. | schedule | L2 | n8n-development-framework |
| [HAIOS - Intel - Disposition](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/intel/haios-intel-disposition.json) | Webhook that records what was decided about an analysis. | webhook | L2 | n8n-development-framework |

### Infra (8)

| Workflow | What it does | Trigger | Level | Repo |
|---|---|---|---|---|
| [AOS - Infra - Site Restore](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/aos-infra-site-restore.json) | Rolls a site back to a known-good commit after a confirmed failure. 15-minute cooldown, 5 restores per 24 hours. | webhook | L2 | n8n-development-framework |
| [AOS-Infra-Site-Validator](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/aos-infra-site-validator.json) | Checks a site on a schedule and calls the restore workflow after a confirmed failure. *(not in production)* | schedule, webhook | - | n8n-development-framework |
| [HAIOS - Infra - CC Config Weekly Digest](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-cc-config-weekly-digest.json) | Weekly Slack digest of open findings about the coding agent's configuration. | schedule | L2 | n8n-development-framework |
| [HAIOS - Infra - Doc Governance](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-doc-governance.json) | Weekly check that workflow folders, snapshots and documentation match what is live. Writes remediation rows. | schedule | L2 | n8n-development-framework |
| [HAIOS - Infra - Log Retention](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-log-retention.json) | Monthly archive-then-prune of resolved remediation rows older than 90 days. Copies them to an archive table first, verifies, then deletes from the hot table. | schedule | L2 | n8n-development-framework |
| [HAIOS - Infra - Remediation Cleanup](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-remediation-cleanup.json) | Deletes stale remediation prompt files and clears their references. | schedule | L2 | n8n-development-framework |
| [HAIOS - Infra - Remediation Trigger](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-remediation-trigger.json) | Counts errors per workflow, catches silent failures, and drafts a remediation prompt when a threshold is met. | webhook, schedule | L2 | n8n-development-framework |
| [HAIOS - Infra - Weekly Audit](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/haios-infra-weekly-audit.json) | Sunday audit of workflow liveness, errors, coverage, backlog, naming, database security and registry gaps. | schedule | L2 | n8n-development-framework |

## SQL and configuration

| File | What it is | Repo |
|---|---|---|
| [sql/rls-policies.sql](https://github.com/MrMinor-dev/database-security-framework/blob/main/sql/rls-policies.sql) | Row-level security state and policies | database-security-framework |
| [sql/rls-audit.sql](https://github.com/MrMinor-dev/database-security-framework/blob/main/sql/rls-audit.sql) | Audit queries for RLS, views and public-role access | database-security-framework |
| [config/write-allowlist.json](https://github.com/MrMinor-dev/database-security-framework/blob/main/config/write-allowlist.json) | Tables and columns the write service may touch | database-security-framework |
| [sql/trust-events.sql](https://github.com/MrMinor-dev/security-governance-framework/blob/main/sql/trust-events.sql) | Trust event log and trust scores | security-governance-framework |
| [sql/drift-detection.sql](https://github.com/MrMinor-dev/security-governance-framework/blob/main/sql/drift-detection.sql) | Calibration and drift queries | security-governance-framework |
| [sql/pgvector-schema.sql](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/sql/pgvector-schema.sql) | Chunk table with HNSW index | rag-knowledge-base |
| [sql/semantic-search.sql](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/sql/semantic-search.sql) | Vector search function | rag-knowledge-base |
| [sql/expenses-and-email-schema.sql](https://github.com/MrMinor-dev/back-office-automation/blob/main/sql/expenses-and-email-schema.sql) | Expense, tax and email tables | back-office-automation |
| [sql/health-and-remediation-schema.sql](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/sql/health-and-remediation-schema.sql) | Health log, registry, remediation log | n8n-development-framework |

## Code and documents

| File | What it is | Repo |
|---|---|---|
| [indexer/semantic_index.py](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/indexer/semantic_index.py) | Incremental indexer | rag-knowledge-base |
| [CHUNKING-RUBRIC.md](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/CHUNKING-RUBRIC.md) | Chunk quality score and document tiers | rag-knowledge-base |
| [GOVERNANCE-CONTRACT.md](https://github.com/MrMinor-dev/security-governance-framework/blob/main/GOVERNANCE-CONTRACT.md) | The contract: 18 laws, 5 tiers | security-governance-framework |
| [enforcement-reference.md](https://github.com/MrMinor-dev/security-governance-framework/blob/main/enforcement-reference.md) | How the laws become actions | security-governance-framework |
| [examples/tier-classifications.md](https://github.com/MrMinor-dev/security-governance-framework/blob/main/examples/tier-classifications.md) | 30 actions sorted into tiers | security-governance-framework |
| [COMPLIANCE.md](https://github.com/MrMinor-dev/security-governance-framework/blob/main/COMPLIANCE.md) | Four kinds of compliance | security-governance-framework |
| [hooks/credential-guard.ps1](https://github.com/MrMinor-dev/security-governance-framework/blob/main/hooks/credential-guard.ps1) | Command hook that blocks credential leaks | security-governance-framework |
| [hooks/safety-guard.ps1](https://github.com/MrMinor-dev/security-governance-framework/blob/main/hooks/safety-guard.ps1) | Command hook that blocks destructive commands | security-governance-framework |
| [hooks/README.md](https://github.com/MrMinor-dev/security-governance-framework/blob/main/hooks/README.md) | How the two hooks work and where they stop | security-governance-framework |
| [templates/session-context.template.md](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/templates/session-context.template.md) | State document template | human-ai-coordination-framework |
| [templates/handoff-contract.md](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/templates/handoff-contract.md) | Handoff and dispatch contracts | human-ai-coordination-framework |
| [schemas/async-command.ts](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/schemas/async-command.ts) | AsyncCommand interface | human-ai-coordination-framework |
| [ARCHITECTURE.md](https://github.com/MrMinor-dev/mcp-server-installation-framework/blob/main/ARCHITECTURE.md) | MCP install protocol | mcp-server-installation-framework |

## Frameworks

See [frameworks/README.md](frameworks/README.md) for the 13 write-ups and 3 worked examples.
