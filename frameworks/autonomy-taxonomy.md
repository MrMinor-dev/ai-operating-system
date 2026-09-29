# Autonomy Taxonomy

**A 10-level scale for how much a workflow can do without a person, with the upgrade step between each level.**

*Status: the scale is in use. The worked example was written for an earlier set of workflows, and 2 of them belonged to a project that has ended. See [examples/agent-assessment.md](examples/agent-assessment.md).*

Every n8n workflow I built was technically autonomous. It ran on a schedule and nobody clicked anything. But a nightly data import and a pipeline that repairs itself are different things, and treating them the same made it impossible to decide what to work on next.

So I gave every workflow a position on a scale. Then I asked the question that mattered: does this one need to move?

## The scale

```
FULL AUTONOMY
  L10  Self-healing and self-improving, runs unattended for months
AUTONOMOUS WITH MONITORING
  L9   Self-healing, plus reporting
  L8   Detects a failure, fixes it, reports it
  L7   Runs alone, alerts when something looks wrong
SUPERVISED
  L6   Runs alone, a human reviews the output
  L5   Runs with guardrails, a human approves key steps
  L4   Mostly automated, a human handles exceptions
MANUAL
  L3   Human-driven, AI assists
  L2   Human-driven, with templates
  L1   Fully manual
```

Each workflow gets 3 tags: `[current level] [status] [target]`. Status is `MAX` (this is the right level, stop) or `WIP` (still improving). Target is `GOAL-L#`.

`L6 WIP GOAL-L8` reads: supervised today, work in progress, aiming for self-healing.

## What it takes to move up

| Step | Requirement |
|---|---|
| L4 to L5 | Input validation and guardrails |
| L5 to L6 | Retry on transient errors |
| L6 to L7 | A "no data collected" check and an alert |
| L7 to L8 | Self-healing: detect the failure, fix it, report it |
| L8 to L9 | Coordination between workflows and awareness of dependencies |
| L9 to L10 | Self-improvement |

## The point of the scale

The instinct is to push everything up. That is wrong.

A workflow that sends a daily summary email doesn't need to repair itself. It needs accurate output and a retry. An L6 with good monitoring is worth more than an L8 that breaks in new ways.

The scale earns its keep when you find the critical path: the chain of workflows where a failure stops the work that matters. An L4 workflow off that path is fine at L4. An L6 workflow on it needs to be L8.

I set the bar for running unattended at L8. It doesn't mean nothing breaks. It means that if something breaks, the workflow fixes it and tells me.

No workflow reached L10. Self-improvement takes more than any single workflow needs. The autonomy of the whole system comes from many L6 to L8 workflows working together.

## Why a scale and not a checklist

A checklist says ready or not ready. A scale says how close, what is missing, and what to build next. It gives a team one word for the state of a thing ("this is an L6"), and it turns "I think it's fine" into "it needs retry logic to reach L7."

The same pattern works wherever maturity is a spectrum and no standard exists yet: cloud migration readiness, DevOps maturity, security posture. Define the levels, name the steps between them, tag the current state, and rank the work by business impact.

## Where it shows up now

Today's workflows carry a related tag in their names: `[L1]`, `[L2]`, `[L3]`. That tag measures error handling. See the [glossary](../GLOSSARY.md). It grew out of this scale but is narrower.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
