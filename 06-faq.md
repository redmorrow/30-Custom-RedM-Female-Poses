# FAQ

Frequently asked questions about the RM 30 Custom Female Pose Pack.

---

## General

**Q: What exactly am I buying?**  
A: 29 custom female pose animations for RedM, delivered as native RDR2 `.ycd` stream files, plus a reference list in `clips.lua` and full documentation.

**Q: Is this a standalone emote script?**  
A: No. This is an **animation asset pack**. It streams the `.ycd` files to your server. You play them through your own emote system or RDR3 natives.

**Q: Does it work on FiveM (GTA V)?**  
A: No. These are RDR2-format animations built exclusively for RedM.

**Q: How many animations are included?**  
A: 29 custom female pose animations, each listed in [03-animation-list.md](03-animation-list.md).

---

## Requirements

**Q: Do I need VORP, RSG, or another framework?**  
A: No. The pack works on any RedM server with no framework dependency.

**Q: Do I need a database?**  
A: No. There are no server scripts and no SQL.

**Q: What is the asset packs dependency?**  
A: The manifest declares `dependency '/assetpacks'` so streamed `.ycd` files are protected through Cfx.re's asset entitlement system. Your server key must have asset packs enabled.

**Q: Do I need RM Emotes?**  
A: No, but RM Emotes is one way to give players access to the poses. You can also use any other emote system or call natives directly.

---

## Usage

**Q: How do I play a pose?**  
A: Use RDR3 natives after the resource is started:

```lua
RequestAnimDict('redmorrow_com@pose5')
while not HasAnimDictLoaded('redmorrow_com@pose5') do Wait(0) end
TaskPlayAnim(PlayerPedId(), 'redmorrow_com@pose5', 'pose5', 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
```

See [02-integration.md](02-integration.md) for full examples.

**Q: Can I add these to my emote menu?**  
A: Yes. Copy the `dict` and `clip` values from `clips.lua` into your emote system's animation table.

**Q: Can I rename poses for my server?**  
A: Yes. Edit `label` and `category` in `clips.lua`. Do not change `dict` or `clip`.

**Q: Can I rename the .ycd files?**  
A: No. RDR2 dictionaries store their internal name. Renaming the files breaks them.

**Q: Can I rename the resource folder?**  
A: No. Keep it as `rm_30-custom-female-pose`.

---

## Licensing & escrow

**Q: Are the animations escrow-protected?**  
A: Yes. The `.ycd` stream files and client logic are encrypted via Cfx.re Keymaster. `config.lua`, `clips.lua`, and documentation remain editable.

**Q: Can I redistribute or resell the .ycd files?**  
A: No. Licensed for use on servers operated by the original purchaser only. See [LICENSE.md](../LICENSE.md).

**Q: Can I use this on multiple servers?**  
A: One licence covers servers you operate. Contact RedMorrow for multi-server licensing.

**Q: Can I share the resource with my developers?**  
A: You may share it with staff who manage your server. Public redistribution is not permitted.

---

## Compatibility

**Q: Does this conflict with other animation packs?**  
A: No, as long as dictionary names do not overlap. This pack uses the `redmorrow_com@` prefix.

**Q: Will this work with photo mode?**  
A: The animations can be triggered while in photo mode if your script or emote system supports it. This pack does not add photo mode features.

**Q: Do poses work on male characters?**  
A: The animations are designed for female character models. They may play on male models but results can look incorrect.

**Q: Do poses work on horseback?**  
A: Full-body poses typically do not play correctly on mounts. Use upper-body flag (`24`) or dismount first.

---

## Support

**Q: Where do I get help?**  
A: Verified purchasers can contact RedMorrow through [redmorrow.com](https://redmorrow.com/). Read [05-troubleshooting.md](05-troubleshooting.md) first.

**Q: Will there be updates?**  
A: Yes. Check [07-changelog.md](07-changelog.md) for version history and update notes.
