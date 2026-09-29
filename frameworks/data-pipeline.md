# Data Pipeline

**Hash the file, skip what hasn't changed, embed only the rest. Keeping a search index current stops being a batch job.**

*Status: running. The code is in [rag-knowledge-base](https://github.com/MrMinor-dev/rag-knowledge-base/blob/main/indexer/semantic_index.py).*

My first index rebuilt everything every time. It embedded the whole corpus to pick up 1 edited file. That took long enough that I only ran it now and then, and then search results went stale, and stale results are worse than no results.

The fix was small. Before embedding anything, compute a hash of the file's content and compare it to the hash stored with its chunks. Same hash, skip. Different hash, replace that file's chunks. On a normal day almost nothing changed, so an update takes seconds and I can run it after every working session.

## The stages

```
1. Find      walk the document folders, skip anything on the exclude list
2. Hash      MD5 of each file's content
3. Compare   against the hash stored in the database for that file
4. Chunk     only files that changed: 750 characters, 150 overlap
5. Embed     in batches of 32, with retries
6. Store     upsert into Postgres, unique on (file, chunk number)
```

The overlap keeps a sentence that lands on a chunk boundary from being cut off from its context. The unique key makes the write safe to repeat. If a run dies halfway, running it again finishes the job.

## Decisions that mattered

**Local to cloud.** The index started in a local ChromaDB. It worked, but only from my machine, and it needed a Python process to be running. I moved it to Postgres with pgvector. That rebuilt everything once. It also meant any n8n workflow could query it, which is what made [search a shared service](semantic-search.md). Judge a migration by what it lets you build afterward, and the cost of doing it is the smaller number.

**A bigger embedding model.** The first version stored 384-dimension vectors. The current one stores 768 with `all-mpnet-base-v2`. Changing models means re-embedding everything, because vectors from different models can't be compared.

**Leaving conversations out.** I once indexed my AI conversation transcripts too. They generated most of the batches and filled the index with conversational filler, so searches for documents came back with chat. The index now holds documents only. The exclude list also keeps out credentials, build logs, and anything named like a secret.

## Numbers today

| Item | Value |
|---|---|
| Documents indexed | 781 |
| Chunk size | 750 characters, 150 overlap |
| Vector size | 768 |
| Index type | HNSW, cosine distance |

## What I would tell a team starting on this

- Hash at the file level. It is cheap and it settles most of the work.
- Make the write idempotent before you make it fast.
- Decide what stays out of the index as carefully as what goes in.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
