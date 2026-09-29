# Multi-Agent Coordination

**One person with one context window hits a ceiling. Parallel agents lift it, if each one has a defined job and a defined boundary.**

*Status: running. Skills and workflows are the coordination layer. The rules below come from the subagent notes I keep for myself.*

Running a business with AI hits the same wall every time. One context window, one thing at a time, everything in sequence. That is an architecture problem, not a tool problem. The answer is parallel agents. But parallel agents with no coordination are just several things going wrong at once.

## Governance first

I wrote the authority tiers, the forbidden-action list, and the skill contracts before the tools could fully use them. The model of a planning layer for decisions and execution agents running in parallel came before those tools were mature. When Claude Code matured, the governance didn't change. The tools stepped into roles that already existed.

Most teams build execution first and add governance after something breaks. Then the authority lines get drawn around whatever the tool already did. Doing it in the other order means the tools fit the roles, and the roles don't bend to fit the tools.

The parallel model: the operator and the planning agent make decisions. Claude Code and other execution agents run work while the next decision gets made. The constraint moves from execution speed to decision throughput, which is the right constraint to have.

## The subagent contract

Every subagent has a spec: what it does, what it takes in, what it produces, which tools it can use, and how to check it worked.

```markdown
---
name: subagent-name
description: One sentence on what this subagent does
model: sonnet
tools: Read, Grep, Glob
---

## Inputs
## Outputs
## Behavior
## Verification
```

Tool access is set by role. Trust doesn't enter into it.

| Role | Tools | Why |
|---|---|---|
| Reviewer | Read, Grep, Glob (Bash for read-only checks) | Can inspect, can't change |
| Builder | Read, Write, Edit, Bash, Grep, Glob | Changes things, from a full spec |
| Researcher | Read, web search, web fetch | Gathers information, no system access |

The workflow auditor is a reviewer. It reads the workflow and scores it. It can't fix anything, and that's deliberate: an auditor that fixes what it finds is grading its own work. It also runs in a fresh context, separate from the agent that built the workflow.

## The handoff contract

What prevents context loss is the dispatch schema: the task, what the agent needs to know, which files to read and write, what success looks like, the authority tier, and where results go. It is a contract and never a summary. The [template](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/templates/handoff-contract.md) is in the coordination repo.

Two patterns run in production. An orchestrator routes each task to a specialist by type. Or agents hand work to each other down a pipeline. Both use the same contract, facts only, so neither side has to trust the other's version of what happened.

## What broke

**Subagents don't inherit the parent's connections.** A subagent I spawned couldn't reach the MCP servers the main session used. It can read local files and run command-line tools. So the parent does the MCP work and hands the subagent the data.

**JSON comes back in code fences.** In 4 of 4 test runs, across 2 model versions, a subagent wrapped its JSON in a Markdown fence even though the instructions said not to. Retrying with a stronger instruction didn't help. The parent's parser now strips fences first.

**A subagent hardcoded a live credential.** I told a verification subagent to read a secret quietly and use it in an API call. It wrote a script with the key as a plain string. The fix is to fetch the data in the parent and pass it inline, so the subagent never handles the credential.

**A search agent can't do structured audits.** An agent built to find files returned a summary when I asked it for a filled-in record per file across 13 files. Search agents locate. They don't inventory.

## Why this matters

Handoff contracts are interface contracts. Once the schema is defined, a new kind of agent slots in without redesigning the coordination layer. The same reasoning applies to microservices, and it applies here.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
