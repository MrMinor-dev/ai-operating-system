# Deployment Protection

**A bad deploy that keeps deploying is worse than the first bad deploy. This is how the site restores itself without looping.**

*Status: running. The workflows are [Site Validator](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/aos-infra-site-validator.json) and [Site Restore](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/infra/aos-infra-site-restore.json). An earlier version protected a different site, and the layers carried over.*

I wanted the business to run while I was away and nobody was watching a dashboard. The failure I worried about wasn't a bad deploy. It was a bad deploy that kept going: the rollback triggers a new deploy, the new deploy fails, and the system loops. Each recovery attempt makes things worse. By the time I looked, the site could be down for days.

The system had to be smart enough to fail well.

## The layers

Each layer covers a blind spot in the one before it.

| Layer | Control | What it does here |
|---|---|---|
| 1. Detect | Validator | Every run checks 4 things: the site root, the blog index, the hosting platform's build status, and the current commit. It records a state: `ok`, `degraded`, or `down`. |
| 2. Confirm | Restore | Before touching anything, Restore checks again. It acts only when the site root and the blog index both fail. One failing check is a false alarm and gets logged as one. |
| 3. Restore | Restore | It rebuilds the repository at the last known good commit, using the hosting API. It doesn't rewind history. It adds a new commit with the old contents. |
| 4. Verify | Restore | It waits 90 seconds and checks the site again. Healthy: it updates state and alerts success. Still down: it alerts a failed restore and marks the state `down`. |
| 5. Limit | Restore | A 15-minute cooldown after each restore. A cap of 5 restores in 24 hours. Hitting either one exits and alerts a person. |

Layer 5 is the one most setups skip. It is what stops a loop.

## Why 3 states and not 2

A boolean healthy/unhealthy would treat a broken blog index the same as a dead site. `down` means the site root fails. `degraded` means the root answers but another check fails. The Validator calls Restore on any failure, and Restore's own confirm step decides. It acts only when both the site root and the blog index are failing, so a degraded site gets logged as a false alarm and left alone.

## Design decisions

**Restore to the last known good commit, not the previous one.** The previous commit might be the broken one. The state table keeps a last known good commit, and Restore targets that.

**Forward commit, not a reset.** Adding a commit that returns to the old contents keeps the full history. Nothing gets rewritten and nothing gets lost.

**Cooldown and a cap, not a rate limit.** A rate limit slows every deploy. Cooldown only applies after a failure, which is the only time cascading is a risk.

**State in the database.** Cooldown, restore count, last known good commit and current state live in one table. Any workflow can ask "is the site safe to deploy to right now?" with 1 query.

## Why this pattern matters

It's defense in depth applied to deployment. Preventive control, detective control, corrective control, and a circuit breaker. Network security uses the same structure: firewall, intrusion detection, endpoint protection, incident response. No single layer is enough. Each covers what the others miss.

| Layer | Catches | Misses |
|---|---|---|
| Detect | Degradation after a deploy | Problems before it |
| Confirm | Transient blips | A failure that only 1 check sees |
| Restore | Confirmed outages | Silent degradation |
| Limit | Cascading restores | An urgent legitimate fix during cooldown |

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
