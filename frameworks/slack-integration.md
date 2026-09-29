# Slack Integration

**Slack in and out. Sending alerts was easy. Receiving commands without an infinite loop took design.**

*Status: running. The workflows are [Slack Inbound](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-slack-inbound-control-plane.json) and [Slack Outbound](https://github.com/MrMinor-dev/n8n-development-framework/blob/main/workflows/comms/haios-comms-slack-outbound.json).*

Outbound alerts were straightforward. Inbound was harder than I expected.

The bot receives its own messages. It sends a message, reads it, processes it, and sends another one. Without filtering, it loops. That isn't an edge case. It is the first thing that happens when you turn on two-way messaging.

## Slack Outbound

The shared send service. Every workflow that needs to alert calls this one, so message formatting and posting live in a single place.

```
Webhook (called by other workflows)
  -> Format message
  -> Post to Slack
  -> Build response
  -> Return response
Error Trigger -> log
```

## Slack Inbound (the control plane)

Two triggers, a Slack event subscription and a chat trigger, feed the same pipeline.

```
Slack trigger / chat trigger
  -> Filter bot messages
       bot:   stop here   (loop prevention)
       human: Parse command
  -> Log to the database (a DB error goes to a shared error handler)
  -> Route by action
       kill    -> execute, confirm
       resume  -> execute, confirm
       status  -> query, format, respond
       help    -> respond
       other   -> general acknowledgment
Error Trigger -> log
```

The filter node is what prevents the loop. If the sender is the bot itself, the message exits immediately.

Every command branch has its own database error path back to a shared handler. A failed `status` query doesn't vanish. It logs and responds.

## What it gives me

I can give the AI instructions without opening a session. Pause everything, resume, check status: from Slack, mid-day, without switching into a full working session. The command shape is the [AsyncCommand schema](https://github.com/MrMinor-dev/human-ai-coordination-framework/blob/main/schemas/async-command.ts).

## Why this matters

Message classification, loop detection, and command parsing are the same problems in any multi-system messaging layer. What differs here is that one participant forgets everything overnight, so every command is logged and the log is the memory.

---

[Back to the hub](../README.md) · Jordan Waxman · [LinkedIn](https://linkedin.com/in/waxmanjordan)
