# RedM 30 Custom Female Pose Pack — Documentation

Get it free - [https://redmorrow.com/products/30-custom-female-pose-animation-pack-free]([https://redmorrow.com/](https://redmorrow.com/products/30-custom-female-pose-animation-pack-free)

Documentation for the RedMorrow **RM 30 Custom Female Pose Pack** (v1.0.0).

## What this resource is

A collection of **29 custom female pose animations** for RedM, streamed as native RDR2 `.ycd` animation dictionaries. The resource registers the animations on your server so any script or emote system can play them through standard RDR3 natives.

This pack provides **animation assets only**. It does not include a player-facing emote menu. You use the poses through your own emote system, job scripts, photography tools, or direct native calls.

## Documents

| Document | Covers |
| --- | --- |
| [01-installation.md](01-installation.md) | Requirements, folder placement, `server.cfg`, first-start verification |
| [02-integration.md](02-integration.md) | Playing poses with natives, animation flags, integrating with emote systems |
| [03-animation-list.md](03-animation-list.md) | Complete table of every pose with dict, clip, and duration |
| [04-configuration.md](04-configuration.md) | `config.lua` and `clips.lua` — what you can edit |
| [05-troubleshooting.md](05-troubleshooting.md) | Symptom-first fixes for streaming, playback, and install issues |
| [06-faq.md](06-faq.md) | Common buyer and server-owner questions |
| [07-changelog.md](07-changelog.md) | Version history |
| [08-support-and-licence.md](08-support-and-licence.md) | Licence summary, supported use, how to get help |

## Start here — new install

1. **Install the resource.** Unzip so the folder is named exactly `rm_30-custom-female-pose`. See [01-installation.md](01-installation.md).
2. **Add to server.cfg.** `ensure rm_30-custom-female-pose`
3. **Verify streaming.** Restart, then test one pose with the native example in [02-integration.md](02-integration.md).
4. **Integrate.** Add the dict/clip entries from [03-animation-list.md](03-animation-list.md) into your emote system. See [02-integration.md](02-integration.md).

## Quick native example

```lua
local dict = 'redmorrow_com@pose5'
local clip = 'pose5'

RequestAnimDict(dict)
while not HasAnimDictLoaded(dict) do Wait(0) end
TaskPlayAnim(PlayerPedId(), dict, clip, 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
```

Flag `1` = loop. See [02-integration.md](02-integration.md) for all play modes.

## Support

Before opening a ticket, read [05-troubleshooting.md](05-troubleshooting.md) and [06-faq.md](06-faq.md). For licence terms see [08-support-and-licence.md](08-support-and-licence.md).

---

Copyright © 2026 RedMorrow · [redmorrow.com](https://redmorrow.com/)
