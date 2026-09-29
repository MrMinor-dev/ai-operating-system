# Document Autonomy

**Documents written for people fail agents. A 9-gate scorecard makes a document's quality something you can measure without reading it.**

*Status: running. The standards are packaged in [doc-management-skill](https://github.com/MrMinor-dev/ai-skills-framework/tree/main/skills/doc-management-skill). The scorecard and a worked example are in [examples/](examples/).*

A person reads "the main workflow" and knows which one you mean. An agent reads the same words and guesses, retrieves the wrong file, or stalls.

The problem grows with the pile. With 20 authoritative documents that overlap, an agent can't tell which one wins, which overrides which, or whether the one it found is still true. It either loads everything and burns tokens, or loads the wrong document and acts on stale information.

"Just keep the docs current" misses the point. A document can be perfectly current and still fail an agent: vague headings, references like "see above," prose that chunks badly in search. Readability for an agent is its own requirement.

## The 3 layers

```
STANDARDS     semantic headers, YAML frontmatter, file-path references,
              chunk-sized sections, a declared source-of-truth status
     |
REGISTRY      every authoritative document listed, with what depends on what
     |
GATES         9 pass/fail checks per document
```

**Naming.** A `-MASTER.md` suffix marks the authoritative source. A document without it can cite the master but never override it. An agent learns that once and applies it everywhere.

## The 9 gates

1. YAML frontmatter is present and complete
2. Source-of-truth status is declared
3. Headers name concepts, not vague topics
4. Cross-references use file paths
5. No ambiguous pronouns (it, this, that) where the referent isn't clear
6. Chunk boundaries fall at logical breaks
7. Version and last-updated are present
8. A registry entry exists
9. Dependencies are documented

The full scorecard is in [examples/9-gate-scorecard.md](examples/9-gate-scorecard.md). A before-and-after in [examples/optimization-example.md](examples/optimization-example.md) shows a document going from 45 to 88 out of 100, with the failed gates listed.

## Two things I learned

**The score is structural.** A small test document and a document 14 times larger reached the same score, because the gates test structure and ignore length. That means quality is auditable without reading the content. Check for the gates.

**Dependencies are the missing layer.** If document A cites document B and B changes, A may now be wrong. Nothing flags it. The registry tracks who depends on whom, so a change to one document lists everything downstream that needs review. That is the difference between a documentation set that stays current and one that slowly drifts.

## Why this matters outside AI

These are the patterns behind configuration management, runbook maintenance and incident playbooks. A difference here is that an agent acting on a wrong document fails right away and in public. A wrong schema document breaks the database call. An outdated skill file runs the wrong behavior. That fast feedback is what keeps the documents right.

The same gates fit any corpus where "is this current and trustworthy?" needs an answer in under 2 minutes: security policy libraries, compliance frameworks, engineering runbooks.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
