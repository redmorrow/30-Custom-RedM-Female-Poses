# RM 30 Custom Female Pose Pack — RedM

**29 custom female pose animations** for RedM, delivered as native RDR2 `.ycd` stream files.

This is an **animation asset pack**. It streams custom pose dictionaries to your server. Use the animations through your existing emote system, job scripts, or RDR3 natives — no framework or database required.

**Author:** RedMorrow · **Version:** 1.0.0 · **Support:** [redmorrow.com](https://redmorrow.com/)

---

## Quick start

1. Copy the `rm_30-custom-female-pose` folder into your server's `resources` directory.
2. Add `ensure rm_30-custom-female-pose` to `server.cfg`.
3. Restart the server (or run `refresh` then `ensure rm_30-custom-female-pose`).
4. Play any pose using RDR3 natives or add the entries from `clips.lua` to your emote system.

```lua
local dict = 'redmorrow_com@pose5'
local clip = 'pose5'

RequestAnimDict(dict)
while not HasAnimDictLoaded(dict) do Wait(0) end
TaskPlayAnim(PlayerPedId(), dict, clip, 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
```

---

## Documentation

| Document | Description |
| --- | --- |
| [docs/README.md](docs/README.md) | Documentation index |
| [docs/01-installation.md](docs/01-installation.md) | Requirements, install steps, verification |
| [docs/02-integration.md](docs/02-integration.md) | Natives, flags, emote system integration |
| [docs/03-animation-list.md](docs/03-animation-list.md) | Full list of all poses (dict / clip names) |
| [docs/04-configuration.md](docs/04-configuration.md) | `config.lua` and `clips.lua` reference |
| [docs/05-troubleshooting.md](docs/05-troubleshooting.md) | Common problems and fixes |
| [docs/06-faq.md](docs/06-faq.md) | Frequently asked questions |
| [docs/07-changelog.md](docs/07-changelog.md) | Version history |
| [docs/08-support-and-licence.md](docs/08-support-and-licence.md) | Licence summary and support |

---

## Requirements

| Requirement | Required |
| --- | --- |
| RedM server (RDR3) | Yes |
| Cfx.re asset packs entitlement | Yes |
| Framework (VORP, RSG, etc.) | No |
| Database | No |
| Emote / animation system | Optional |

---

## What's included

- `stream/*.ycd` — custom animation dictionaries (escrow-protected)
- `clips.lua` — animation reference list (editable)
- `config.lua` — basic settings (editable)
- `docs/` — full documentation
- `LICENSE.md` — end user licence agreement

---

## Licence

Copyright © 2026 RedMorrow. All rights reserved. See [LICENSE.md](LICENSE.md) and [docs/08-support-and-licence.md](docs/08-support-and-licence.md).
