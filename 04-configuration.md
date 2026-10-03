# Configuration

What you can edit in `config.lua` and `clips.lua` after purchase.

Both files remain **readable and editable** after Cfx.re Keymaster escrow. The streamed `.ycd` files and client logic are protected.

---

## clips.lua

The animation reference list. Each entry defines one pose:

```lua
{
    id         = 'pose5',                  -- short identifier
    label      = 'pose5',                  -- display name (editable)
    dict       = 'redmorrow_com@pose5',   -- dictionary — DO NOT CHANGE
    clip       = 'pose5',                  -- clip name — DO NOT CHANGE
    category   = 'pose5',                  -- grouping label (editable)
    duration   = 1.967,                    -- length in seconds (reference)
    mode       = 'loop',                   -- suggested: 'once' | 'loop' | 'hold'
    rootMotion = false,                    -- true if clip moves the character
}
```

### Safe to edit

| Field | Purpose |
| --- | --- |
| `label` | Name shown in your emote system or logs |
| `category` | Group poses (e.g. `"Portrait"`, `"Saloon"`, `"Casual"`) |
| `mode` | Suggested playback mode for integration scripts |
| `walk` | Set `true` if pose works best as upper-body only |

### Do not edit

| Field | Why |
| --- | --- |
| `dict` | Must match the `.ycd` file name exactly |
| `clip` | Must match the clip name stored inside the `.ycd` file |

Changing `dict` or `clip` to incorrect values causes `DoesAnimDictExist` to fail or the animation to refuse to play.

---

## config.lua

Basic resource settings:

```lua
Config.Title = 'Female Poses'           -- resource display title
Config.Dict  = 'redmorrow_com@pose5'  -- fallback dictionary (rarely used)
```

These values are mainly for internal reference when integrating with helper scripts. The animation pack itself does not require configuration to stream the `.ycd` files.

---

## Escrow — what stays editable

After Keymaster upload:

| Editable (escrow_ignore) | Protected |
| --- | --- |
| `config.lua` | `client.lua` |
| `clips.lua` | `stream/*.ycd` |
| `README.md`, `LICENSE.md` | Other protected scripts |
| `docs/*.md` | |

You can customize labels, categories, and documentation freely. You cannot extract or modify the `.ycd` animation data.

---

## Restart after changes

`clips.lua` and `config.lua` are loaded when the resource starts. After editing either file:

```
restart rm_30-custom-female-pose
```

Or restart the full server.

---

## Next steps

- Integration examples: [02-integration.md](02-integration.md)
- Full pose table: [03-animation-list.md](03-animation-list.md)
