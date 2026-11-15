# Cost notes

## The 402 lesson

On 2026-11-14 a bot running a paid Claude Sonnet model spent **$7.12 in under an hour** of tool calls, then failed mid-task with **HTTP 402** when the provider balance ran out. The task produced nothing and had to be re-run on a cheap model.

Two conclusions, now kept as rules:

1. **Cheap by default.** Bulk work runs on a cheap flash model. A larger model only where judgment pays for itself, and never as a default.
2. **Per-hour cost before the switch.** Anything that could run 24/7 is priced per hour first. A model that costs money while idle is a bill, not a feature.

## What to say when switching

- The model name, exactly as the app lists it.
- Rough cost per hour of heavy use.
- The fallback model.
- Whether the account needs a top-up to work at all.

## Reminder

A phone or tablet app cannot change models or keys. That is by design — "Only on your computer". Do not spend a turn rediscovering it.
