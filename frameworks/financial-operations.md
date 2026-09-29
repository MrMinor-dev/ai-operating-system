# Financial Operations

**What does the AI get to do with money? I answered that in writing before it touched anything.**

*Status: running. The workflows are in [back-office-automation](https://github.com/MrMinor-dev/back-office-automation/tree/main/workflows/finance).*

Running a business with AI forces a question most teams put off. What is the agent allowed to do with money? Not in theory. In writing, before it touches anything.

I drew the line at $0 of spending authority. The agent can record, categorize, and alert. Anything that moves money stops and waits for me. That one decision shaped 3 workflows.

## Expense Entry

[Expense Entry](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-expense-entry.json) takes an expense over a webhook. Two gates sit in front of the database.

```
Webhook
  -> Validate required fields   (bad: reject)
  -> Map to an IRS tax category
  -> Check the input again      (bad: reject)
  -> Insert into Postgres
  -> Respond
```

Tax category mapping happens at entry. It's not a year-end batch. Bad input is caught before it reaches a table.

## Budget Monitor

[Budget Monitor](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-budget-monitor.json) runs each morning and on demand. It reads month-to-date expenses, computes budget status, and decides whether to alert. Before it sends anything, it checks alert history. That step keeps the same breach from alerting every day.

## Invoice Handler

[Invoice Handler](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-invoice-handler.json) turns invoice emails into expense rows. The [email intelligence write-up](email-intelligence.md) covers how it gets there.

## The line at $0

The $0 line is a governance decision, made before any code existed. It isn't a technical limit. Under $0 the agent tracks, categorizes, and alerts. Over $0 it stops. The system is built so that boundary is hard to cross by accident.

Financial automation for a real business needs 2 things: the workflows that handle the routine, and the explicit boundary that says where automation ends. Tools make the first easy. The second is an architecture decision, and skipping it means you made it by default.

This is the [Tier 1 rule](https://github.com/MrMinor-dev/security-governance-framework) in practice: money is always approval-required at minimum.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
