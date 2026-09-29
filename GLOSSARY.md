# Glossary

Terms and labels used across the repos.

## Roles

**CEO and COO.** Labels for who decides what. I am the CEO: I own strategy, all spending, external relationships, and final say. The AI agent is the COO: it executes approved work, keeps documentation accurate, watches workflow health, and escalates anything outside its authority. The labels are borrowed from an org chart so the split is easy to remember. They are not role-play. The [governance contract](https://github.com/MrMinor-dev/security-governance-framework/blob/main/GOVERNANCE-CONTRACT.md) defines them.

**Claude, Claude Code.** Claude is the model I work with in chat sessions, mostly on planning and strategy. Claude Code is the same family of model working in a terminal, mostly on building and running things. In the files you may see "CC" for Claude Code.

**Operator.** The human. Used when a rule applies to the human role and not to me in particular.

## Authority tiers

Every action the agent can take sits in one tier. When it can't tell which, it takes the higher one.

| Tier | Name | What happens |
|---|---|---|
| 0F | Forbidden | Never runs, whatever the instruction |
| 0H | Human-only | The human does it directly |
| 1 | Approval required | Agent proposes, human approves first |
| 2 | Inform after | Agent acts, then reports |
| 3 | Autonomous | Agent acts |

## Workflow maturity levels (L1, L2, L3)

Every workflow name ends in a level tag such as `[L2]`. The tag says how much error handling the workflow has.

| Level | What it means |
|---|---|
| L1 | Logs a health check on success |
| L2 | Also has an Error Trigger that logs errors |
| L3 | Also calls the Remediation Trigger, so failures start a fix without waiting for a person to notice |

The [65-point audit](https://github.com/MrMinor-dev/ai-skills-framework/tree/main/skills/n8n-workflow-audit) scores this in its remediation maturity category.

## System names

**HAIOS.** Human-AI Operating System. Layer 0: the working relationship between the operator and the agent. State documents, handoffs, async commands.

**AOS.** Agentic Operating System. Layer 1: the platform. Workflows, database, skills, search.

**Agency.** A client-facing layer built on top of the platform. Its workflows are not published here because they touch client data paths.

Workflow names follow the pattern `LAYER: Domain - Capability [Level]`.

## Other terms

**Skill.** A Markdown file with a name, a description that says when to use it, and step-by-step instructions. The agent reads it before doing the job. Skills are versioned.

**Skill drift.** A skill's behavior slowly moving away from its written spec because the model fills gaps from memory. Reading the file each time stops it.

**SSOT.** Single source of truth. Each piece of knowledge has one authoritative home. Everything else points to it.

**RLS.** Row-level security. A Postgres feature that decides, per row, which roles can see or change it.

**MCP.** Model Context Protocol. A standard way to give an AI tool access to outside systems.

**RAG.** Retrieval-augmented generation. The model looks up relevant text first, then answers from it.

**Handoff contract.** A fixed schema for passing work between agents or skills. Facts only: what was done, which files changed, what to do next.

**Health table.** The one Postgres table every workflow writes to. Success and error rows land in the same place.

**Remediation.** A logged fix for a detected problem, with a status: pending, fixed, dismissed, or abandoned.
