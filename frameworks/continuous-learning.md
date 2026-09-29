# Continuous Learning

**Outside signals go in, analyses come out, and the operator decides what happens to each one.**

*Status: running. This is the Intel system, 6 workflows in the [n8n repo](https://github.com/MrMinor-dev/n8n-development-framework/tree/main/workflows/intel).*

A business that runs on AI tools sits on a moving stack. The platforms change. The vendors ship new features. Rules shift under you. If nobody is watching, you find out when something breaks.

I built a pipeline that watches for me and puts the result in front of me in the morning.

## The pipeline

```
Collectors (nightly)
  vendor release feeds, social and blog sources, platform and vendor email
      |
      v
Intel tables
      |
      v
Analyzer (nightly): Claude, plus semantic search over the business documents
      |
      v
Analysis rows --> Daily Digest and Weekly Report in Slack
      |
      v
Operator decides --> Disposition webhook records the decision --> back into the Analyzer
```

**Collect.** Three collectors run nightly: vendor release feeds, social and blog sources, and platform and vendor email. Each writes raw signals into shared tables and skips what it has already seen. A fourth workflow, the n8n Metrics Collector, stores execution stats every 6 hours.

**Analyze.** The Analyzer reads new signals. It searches the knowledge base for the documents that relate to each one, so the analysis knows what the business already does. Claude classifies the signal and writes an analysis row.

**Surface.** The Daily Digest lists new analyses. The Weekly Report adds the landscape view.

**Decide.** The Disposition workflow is a small webhook. When I decide what to do about an analysis, it records the decision. The record feeds the next round: the Analyzer reads disposition history, so earlier decisions inform each new analysis.

## Why the loop matters

Most systems treat knowledge as a byproduct of doing the work. Here it is a workflow with an owner. Signals feed analysis. Analysis feeds decisions. Decisions feed the next analysis.

The second loop is on the failure side. When production breaks something, the fix becomes a rule, and the rule goes into a skill or an audit check. That is how the [65-point audit](https://github.com/MrMinor-dev/ai-skills-framework/tree/main/skills/n8n-workflow-audit) grew.

## What I would tell a team starting on this

- Store the decision alongside the analysis. Without it, the system raises the same thing forever.
- Put the analyst in the loop early. Claude is good at first-pass classification and bad at knowing what matters to your business.
- Give each collector one job and one table. Debugging is easier.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
