# Semantic Search

**Search before you load. Find the right paragraph first, and open the whole file only when the paragraph says it's worth it.**

*Status: running. SQL, workflow and schema are in [rag-knowledge-base](https://github.com/MrMinor-dev/rag-knowledge-base).*

Two weeks in, results got worse. Searches that should have found strong matches returned weak ones. Nothing errored. Nothing alerted.

The embedding provider had moved to a new URL format. The old address kept accepting requests and kept returning vectors. The vectors just weren't accurate anymore. The only signal was that answers got worse.

That failure shaped the design: retrieval needs health signals, and uptime checks alone don't count as one.

## The problem it solves

An agent working across a large document set has 3 bad options.

- **Load everything that might matter.** That burns the context window before the work starts.
- **Search by file.** Finding the right document isn't enough. You need the right paragraph in it.
- **Rebuild the index on every change.** That's too slow to keep current.

Semantic search answers the first two. The [data pipeline](data-pipeline.md) answers the third.

## How it works

1. The agent, or a workflow, sends a question to a webhook.
2. The workflow turns the question into a vector with the same model that embedded the documents.
3. A Postgres function returns the closest chunks by cosine distance, above a similarity threshold, with their file paths.
4. The caller reads the chunks and cites where they came from. It opens the full file only if the chunks confirm it's the right one.

```sql
SELECT content, file_path, 1 - (embedding <=> query_embedding) AS similarity
FROM doc_embeddings
WHERE 1 - (embedding <=> query_embedding) > 0.5
ORDER BY embedding <=> query_embedding
LIMIT 5;
```

`<=>` is pgvector's cosine distance. Subtracting from 1 turns distance into similarity. The threshold cuts results that are unrelated to the question. An HNSW index keeps the lookup fast by searching for near neighbors instead of scanning every row. The real function is in [sql/semantic-search.sql](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/sql/semantic-search.sql).

## Problems I hit

**The silent endpoint move.** Described above. I added retrieval health-check queries to my weekly checklist.

**A runtime that was too new.** The newest Python release wasn't supported by the embedding library's dependencies. Dropping back one version fixed it. Bleeding-edge runtimes and machine-learning libraries don't mix.

**Log lines in the protocol stream.** A search server talked to its host over standard output. A stray log line corrupted the stream, and the errors were intermittent because only some code paths logged. The fix was to keep logging and communication on separate channels. It's the same failure the [MCP installation repo](https://github.com/MrMinor-dev/mcp-server-installation-framework) covers.

**One function, two payload shapes.** The same search received input differently from an MCP call than from a webhook. Failures were intermittent. Every utility workflow now checks both shapes at the door.

**An off-by-one in batching.** An update loop silently dropped the last batch when the file count didn't divide evenly. I caught it by comparing expected and actual chunk counts after indexing.

## What I would tell a team starting on this

- Test retrieval quality on a schedule. A quiet failure looks exactly like a working system.
- Return file paths with every chunk so the reader can check the source.
- Put the index where every part of the system can reach it.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
