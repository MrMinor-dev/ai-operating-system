# Session Continuity

**An AI operator forgets everything when the conversation ends. This is the system that lets it pick up where the last session stopped.**

*Status: running. The state document template is in [human-ai-coordination-framework](https://github.com/MrMinor-dev/human-ai-coordination-framework). The session skills are in [ai-skills-framework](https://github.com/MrMinor-dev/ai-skills-framework).*

Session-based AI agents have amnesia. Each conversation starts from zero, and 4 things go wrong because of it.

- **Context loss.** The agent doesn't know what happened yesterday, what is in progress, or what failed last time. Every session spends tokens re-explaining.
- **Silent degradation.** With no memory, the agent can't see patterns across sessions: repeating bugs, drifting priorities, piling technical debt.
- **Abrupt cutoffs.** Token limits are invisible to both sides. The agent says there's plenty of room, then hits the wall mid-task and loses what wasn't saved.
- **Ramp-up tax.** A slice of every session goes to getting the agent back to where the last one ended.

The usual answer is more context. Dumping every document into the window burns the budget before the work starts. You need selective retrieval.

## The 4 layers

```
1. Living state document    one file, rewritten each session, read first
2. Session protocols        startup, start-of-day and end skills
3. Semantic retrieval       search the document index before loading files
4. Context discipline       know what a load costs before you do it
```

**Layer 1: the state document.** One file is the ground truth. It has 5 sections: what is next, the workstreams and their state, recent session history, flags, and reference data. It is rewritten each session, not appended to, and old entries roll off. It answers 3 questions: what is happening now, what is next, what could go wrong. An agent that reads it knows what to do without asking. The [blank template](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/templates/session-context.template.md) is published.

**Layer 2: session protocols.** Three skills keep every session consistent. The startup skill reloads state and routes to a focus area. The start-of-day skill gives a fuller briefing on the first session of the day. The end skill records decisions, updates the state document, flags unfinished work, and hands off. The agent never just stops.

**Layer 3: semantic retrieval.** When the state document isn't enough, search finds the relevant chunk without loading whole files. See [semantic search](semantic-search.md). The rule of thumb: search first, load the full file only if the chunk says it's the right one.

**Layer 4: context discipline.** Born from an incident. The agent auto-loaded a large block of context, said there was plenty of room, and ran out minutes later. It lost everything unsaved. The cause was that nobody, human or agent, could see how much was being spent. The fix was to estimate the cost before loading, search before loading, and checkpoint before the limit and not after.

## The lesson

Building the state document was the easy part. Getting the agent to use it every time was harder.

Without enforced protocols the agent skips the startup read to save tokens, forgets to update at the end because the conversation just stopped, or loads everything to be thorough. Every layer exists because a specific failure happened first.

- Layer 1: the agent kept re-asking questions it already had answers to.
- Layer 2: sessions ended without a record of what had happened.
- Layer 3: loading everything wasn't sustainable.
- Layer 4: a session died mid-task and took its work with it.

The system doesn't rely on the agent remembering to do the right thing. It makes the right thing the default path.

## Failures that shaped it

**Context ran out mid-task.** Described above. It produced layer 4.

**The history file was overwritten.** A skill wrote a file when it should have appended. It destroyed months of accumulated history, and I recovered part of it from the search index. The fix was to state the write mode explicitly in every skill. The lesson I wrote down: ambiguous instructions default to destructive behavior.

**The agent read a stale state document.** It made decisions on out-of-date priorities. The lesson: a state document nobody maintains is a liability, so the end-of-session update is not optional.

## Why this matters

It is incident response applied to AI. The context failure followed the same arc as any outage: something failed, neither side could see why, the cause was a gap in visibility, and the fix was monitoring with defined checkpoints. The overwrite was a destructive-default bug: an ambiguous instruction, no write-mode check, an action that can't be undone. Both changes are permanent and both are written down.

Any system that runs on its own needs state management, handoffs, and enforced behavior, on top of capability. An agent that does the work but can't hand off cleanly is a reliability problem.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
