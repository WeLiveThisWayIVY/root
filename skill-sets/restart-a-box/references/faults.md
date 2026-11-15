# Known faults

Match on the text in the left column. The fix is only correct for that line.

| What you see | Cause | Fix |
| --- | --- | --- |
| `Unit openmausbot.service could not be found` | Looking at the system unit, not the user one | `systemctl --user status openmausbot` |
| Model list empty, or only one model | App build older than the model catalog | `npm i -g --prefix ~/.local openmausbot@latest`, then `systemctl --user restart openmausbot` |
| Model list still empty after updating | The model is chosen on the box, not the phone | Change it in the app running on the box; the phone app says "Only on your computer" by design |
| `browser: Chrome could not be prepared` | Ubuntu's AppArmor blocks unprivileged user namespaces | Drop-in `/etc/sysctl.d/99-userns.conf` with `kernel.apparmor_restrict_unprivileged_userns=0`, then `sudo sysctl --system`, then restart the unit |
| Tunnel gone after a reboot | `cloudflared` not enabled as a service | `sudo systemctl enable --now cloudflared`, verify with `systemctl status cloudflared` |
| Hostname returns 403, "forbidden: this request came through a proxy" | Healthy — the tunnel is reaching the box, the device simply is not paired | Nothing. This is the working answer |
| `You have no Local VM desktop in this turn` | No Local VM installed, and a bot cannot install its own | Build it from the app's own Local VM panel on the box, not by pulling an image name |
| `HTTP 402` mid-task | Provider credit ran out | Switch to a cheap model on the box and top up; keep per-hour spend visible |

## Notes

- The tunnel runs a dashboard-managed configuration via `--token-file /etc/cloudflared/token` as the desktop user, not root.
- Chrome's binary may not be at `/opt/google/chrome/chrome`, so an AppArmor profile written for that path will not apply.
