# Knowledge Mining

**Structured evidence from unstructured history: define what you need first, then write the queries against that.**

*Status: a method I ran once, with results I still use. The conversation corpus it ran on is no longer in the search index. See the [data pipeline](data-pipeline.md).*

Most organizations sit on years of history nobody interrogates: meetings, decisions, incident reports, retrospectives. The patterns and the institutional knowledge are in there. They aren't structured, so nobody can act on them.

I had a small version of the same problem. Hundreds of AI conversations, every architectural decision and every debugging session, all buried in text. I needed a structured inventory of what I had actually done, for a resume, and I wasn't going to reconstruct it from memory.

## The method

**1. Make it retrievable.** You can't mine what you can't search. The history went into a vector index first. This is the prerequisite.

**2. Write the schema before the queries.** I took a real job description and broke it into 9 categories of evidence: cross-functional program execution, technical depth, and so on. The query set was the mining plan.

The difference between schema-driven and open-ended querying is the difference between extraction and hope.

```
# Open-ended: produces noise
query: "good things I've done"

# Schema-driven: produces evidence
schema: Cross-Functional Program Execution
query: "multi-domain coordination program management cross-functional"
query: "stakeholder alignment competing priorities dependencies"

schema: Technical Depth
query: "architecture design decision tradeoffs production system"
query: "debugging failure root cause fix production workflow"
```

**3. Extract and distill.** Each result either supports a requirement or it doesn't. I reviewed every result against the schema, pulled out accomplishments, and attached the source excerpts to each.

The output is an accomplishment inventory where every item traces to source material. Nothing is reconstructed from memory.

## The pattern for other organizations

The inputs change: support transcripts, sales calls, incident logs, post-mortems. The steps don't.

1. Embed and index the corpus.
2. Define the structured output you need.
3. Write queries against that structure.
4. Extract, review, distill.

The companies that move fastest with AI won't be the ones that automate tasks first. They'll be the ones that instrument their operations so the history compounds. Every session and every workflow run leaves a record. Mining is what turns the record into intelligence.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
