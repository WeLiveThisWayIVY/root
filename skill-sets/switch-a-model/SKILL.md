---
name: switch-a-model
description: Use when changing which model or API key a bot runs on. The change happens on the box itself, because the phone and tablet apps cannot do it ("Only on your computer"). Carries the cost rule that keeps a cheap model from turning into a large bill.
---

# Switch a model

## The rule up front

**Changes happen on the box, never from the phone or tablet app.** The mobile app shows "Only on your computer" by design. Retrying there is wasted time, not a bug.

## Steps

1. **Decide the model, and say why in one line.** Cheapest that does the job; name the reason in the person's terms ("Flash for bulk scanning, a bigger model only where judgment pays").
2. **Do it on the box.** Change the model in the app running on the box's own desktop, or edit the same setting in the box's config. If the person only has a shell, give them the exact file and line rather than "change the model in settings".
3. **Update the app first if the model is not in the list.**
   ```bash
   npm i -g --prefix ~/.local openmausbot@latest
   systemctl --user restart openmausbot
   ```
4. **Restart the unit so the change takes.**
   ```bash
   systemctl --user restart openmausbot
   ```
5. **Verify it took.** The model shown in the box's own app is the new one, and a test message comes back running on it. The click alone is not proof.
6. **Say what it costs.** One line: model name, rough cost per hour of heavy use, the fallback model, and whether the account needs a top-up to work at all.

## Do not

- Do not try to change the model from the phone or tablet app.
- Do not assume one box's model list matches another's — each box has its own.
- Do not switch to a big model "to be safe" without stating the per-hour cost first.
- Do not leave the old key on the box after replacing it.
- Do not report the switch done before a test reply comes back on the new model.

## Reporting line

"Switched **<bot>** to **<model>** on **<box>**. Verified: <test reply or model shown>. Cost: ~<x> per hour at heavy use; fallback <model>."
