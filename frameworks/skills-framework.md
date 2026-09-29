# Skills Framework

**Autonomous work needs defined, versioned procedures the agent reads before it acts. Skills are how that works here.**

*Status: running. All 25 current skills are in [ai-skills-framework](https://github.com/MrMinor-dev/ai-skills-framework). That repo's README covers the mechanics. This page is the design thinking.*

A skill is a versioned capability module. It has a name, a description with exact trigger phrases, a step-by-step workflow, an authority tier, error handling, and a handoff statement that says what it produced. The contract is read before every run. Consistency comes from the read, and never from the agent's memory.

## What made the contract concrete

A skill destroyed months of organizational history. The session-end skill was supposed to append to a running log. It overwrote it. The instructions never said which, and "save to file" is ambiguous. The agent made a reasonable choice, and the choice was wrong. I recovered part of the history from the search index. The rest was gone.

Two permanent changes came out of it. Every skill now states the write mode for any file operation. And the skill that builds skills added structural validation, so a skill can't ship without required fields, explicit write modes, error handling, and a handoff statement.

## Triggers are a precision instrument

A trigger that's too broad fires on things it shouldn't. One that's too narrow gets missed. "Start session" and "new session" trigger startup. The bare word "session" doesn't, because it would match dozens of unrelated mentions. Each trigger phrase is unique across skills, and the creator skill checks for overlap before a new skill goes in.

## Version numbers count evidence

`skill-creator-skill` is on version 3.8. Each version exists because real use found a real gap: vague trigger rules, no token-budget check, structure nobody validated until a skill failed. Skills carry a section on anti-patterns, and those are failures that happened.

## Skills that build skills

The creator skill follows the same contract as the skills it builds. It runs a creation workflow, checks trigger uniqueness, enforces a size budget, and runs a structure checklist before anything goes to production.

## The shape of a skill

```
skill-name/
  SKILL.md          frontmatter (name, description with triggers),
                    workflow, handoff contract, authority, error handling
  references/       detail loaded only when a step needs it
```

## Why this matters

A skill contract is a standard operating procedure for a team where one member forgets everything overnight. If the procedure isn't read before the work, the agent works from memory, and memory resets.

SOPs and skill contracts fail the same way: an under-specified instruction gets filled in by whoever runs it, using a reasonable-looking default. With an AI there's nobody to ask. The default runs immediately. So the contract has to be complete before the skill ships.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
