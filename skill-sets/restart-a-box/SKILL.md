---
name: restart-a-box
description: Use when an OpenMausBot box is broken or behaving oddly — service down, empty model list, Chrome won't start, or the tunnel stopped answering. Diagnoses and fixes it layer by layer, checking each one.
---

# Restart a box

## Ground rules

- OpenMausBot normally runs as a **user-level** unit. Use `systemctl --user`, never `sudo systemctl`.
- The person may only be able to paste commands into a shell. Give one self-contained block at a time, and ask for its output before the next step.
- Fix the layer that is broken. Do not reinstall to avoid a diagnosis.

## Steps

1. **Ask what is wrong, in one line.** "What do you see — an error, a blank list, or nothing at all?" The symptom picks the row in the fault table; do not guess.
2. **Check the unit.**
   ```bash
   systemctl --user status openmausbot --no-pager
   ```
   `active (running)` means the service is up and the problem is above it. `failed` or `inactive` goes to the restart:
   ```bash
   systemctl --user restart openmausbot
   ```
3. **Check the build is current** when the symptom is a missing feature or an empty model list:
   ```bash
   npm i -g --prefix ~/.local openmausbot@latest
   systemctl --user restart openmausbot
   ```
4. **Match the symptom against the fault table** in [references/faults.md](references/faults.md). Each row begins with the exact text to look for. Apply the stated fix only after the log line matches — a similar-looking symptom with a different line is a different fault.
5. **Verify from outside** when the fault was connectivity:
   ```bash
   curl -sI https://<host> | head -1
   ```
   A `403` carrying "this request came through a proxy" is a **healthy** answer for an unpaired device. A timeout is the failure. Do not call a working tunnel broken because it is not a 200.
6. **Report** in this shape: what was wrong, what you changed, and the command that proves it is fixed.

## Do not

- Do not use `sudo systemctl`. The unit is under the user.
- Do not try to change the model from the phone app — it cannot, by design.
- Do not re-tag or re-pull a Local VM image to fix a build. Compatibility is decided by labels, and a bot cannot install its own Local VM.
- Do not reinstall the app to fix a fault the log line already names.
- Do not call a 403 tunnel broken.

## Reporting line

"Fixed: **<fault>**. Cause: <one line>. Proof: `<command>` → <output>. Nothing else changed."
