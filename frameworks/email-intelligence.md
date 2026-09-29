# Email Intelligence

**Structured records from an unstructured inbox: sort by rule, extract by pattern, and keep the AI out of the path until a person has to decide.**

*Status: running. The workflows are in [back-office-automation](https://github.com/MrMinor-dev/back-office-automation/tree/main/workflows/email).*

Every business has the same inbox. Invoices that need logging. Notices that need attention today. Vendor updates worth tracking. Noise that should disappear. The default fix is a person reading every message and deciding.

An earlier version of this system asked Claude to classify each email. It worked. But it put a model call on every message for a decision that mostly turned on who sent it. The current version uses rules, and rules are easier to audit.

## Email Router

The [Email Router](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/email/aos-email-email-router.json) fires on each incoming Gmail message, or on a webhook. A rules classifier checks the sender's domain against lists: platforms, financial institutions, infrastructure vendors, and so on. It labels the message, marks it read, and either moves it out of the inbox or leaves it. It is a pure router. It doesn't act on the message.

A backfill path labels old messages that were never sorted. Errors from every branch merge into one error handler, so a failure is logged wherever it happened.

Adding a new kind of sender is 1 line in a list. It doesn't need a new prompt or a new model test.

## Invoice Handler

The [Invoice Handler](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/finance/aos-finance-invoice-handler.json) runs every morning on the messages the Router labeled financial. It reads the message body, extracts vendor, amount and dates by pattern, skips things that look like statements and not invoices, and writes an expense row. It also removes the financial label, so the same message isn't processed twice.

## Quarantine Manager

The [Quarantine Manager](https://github.com/MrMinor-dev/back-office-automation/blob/main/workflows/email/aos-email-quarantine-manager.json) handles quarantined messages. It posts a daily digest to Slack and archives the ones that have expired.

## What I would tell a team starting on this

- Start with rules. Most routing turns on sender and subject, and rules are auditable. Bring in a model where the input really is free text.
- Classify once and route by rule. Adding a category should be 1 line.
- Give the failure paths the same attention as the success path. The inbox is where silent failures hide.

The same shape fits any stream of unstructured input that has to become records: support tickets, vendor mail, compliance filings.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
