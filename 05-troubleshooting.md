# Troubleshooting

Symptom-first guide for common problems with the RM 30 Custom Female Pose Pack.

---

## Resource won't start

### "Failed to load resource" / asset pack error

**Cause:** Server lacks Cfx.re asset packs entitlement.

**Fix:**
- Confirm your server licence key has asset packs enabled in the Cfx.re portal.
- The manifest declares `dependency '/assetpacks'` — this is required for streamed `.ycd` files.

### Resource name error

**Cause:** Folder was renamed.

**Fix:** Rename the folder back to exactly `rm_30-custom-female-pose`.

---

## Animation dictionary not found

### `DoesAnimDictExist('redmorrow_com@pose5')` returns false

**Checklist:**

1. Is the resource started?
   ```
   ensure rm_30-custom-female-pose
   ```
2. Is it in `server.cfg`?
3. Did you run `refresh` after adding the resource?
4. Is the `.ycd` file present in `stream/` with the correct name?

### Console message: "Animation dictionary is not streamed"

**Cause:** Resource not running, or dict name typo.

**Fix:**
- Verify resource is started: check server console for green `Started resource rm_30-custom-female-pose`.
- Double-check dict name against [03-animation-list.md](03-animation-list.md).
- Remember: `pose29` uses dict `redmorrow_com@pose26`, not `redmorrow_com@pose29`.

---

## Animation won't play

### Dictionary loads but character does nothing

**Possible causes:**

| Cause | Fix |
| --- | --- |
| Wrong clip name | Verify clip in [03-animation-list.md](03-animation-list.md) |
| Ped is dead / ragdoll / swimming | Animation blocked by game state |
| Ped on horseback | Dismount or use upper-body flag (`24`) |
| Wrong flag for mode | Use flag `1` for loop, `0` for once, `2` for hold |
| GTA V flags used | RDR3 flags differ — see [02-integration.md](02-integration.md) |

### Clip plays but looks wrong / T-pose flash

**Cause:** Dictionary still loading when `TaskPlayAnim` was called.

**Fix:** Always wait for `HasAnimDictLoaded(dict)` before playing:

```lua
RequestAnimDict(dict)
while not HasAnimDictLoaded(dict) do Wait(0) end
TaskPlayAnim(...)
```

### Animation stops immediately

**Cause:** Using flag `0` (once) on a very short clip, or another script clearing ped tasks.

**Fix:** Use flag `1` (loop) or `2` (hold) for pose animations.

---

## Integration issues

### Emote menu doesn't show the new poses

**Cause:** Entries not added to your emote system's database or config.

**Fix:** This pack streams animations only. You must manually add dict/clip entries from `clips.lua` into your emote resource. See [02-integration.md](02-integration.md).

### Works in test script but not in emote menu

**Cause:** Emote system uses different dict/clip names, or resource start order.

**Fix:**
- Ensure `rm_30-custom-female-pose` starts before or with your emote resource.
- Copy exact `dict` and `clip` values from [03-animation-list.md](03-animation-list.md).

---

## File issues

### Renamed .ycd files

**Symptom:** Dictionary missing or clip not found.

**Fix:** Restore original file names. RDR2 dictionaries embed their own name — renaming breaks them.

### Missing stream files

**Symptom:** Some poses work, others don't.

**Fix:** Compare your `stream/` folder against the file list in [03-animation-list.md](03-animation-list.md). Re-download from Keymaster if files are missing.

---

## Performance

### Server lag

This resource has **no server scripts** and **no database queries**. It cannot cause server-side lag. All streaming is client-side.

### Client stutter on first play

**Cause:** First-time dictionary load from stream.

**Fix:** Normal behavior. Subsequent plays of the same dictionary are instant. Pre-load with `RequestAnimDict` before the player needs the pose.

---

## Before contacting support

Gather this information:

1. RedM server artifact version
2. Full server console output when starting `rm_30-custom-female-pose`
3. F8 client console errors when trying to play a pose
4. Exact dict and clip names you are using
5. Which emote system you integrate with (if any)
6. Confirmation that `DoesAnimDictExist('redmorrow_com@pose5')` returns true or false

See [08-support-and-licence.md](08-support-and-licence.md) for contact details.
