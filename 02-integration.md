# Integration Guide

How to play the custom female pose animations on your RedM server.

## Overview

Once `rm_30-custom-female-pose` is started, all `.ycd` dictionaries in `stream/` are registered automatically. The dictionary name is the file name without `.ycd`:

```
stream/redmorrow_com@pose5.ycd  →  dict: 'redmorrow_com@pose5'
```

Every dict/clip pair is listed in `clips.lua` and [03-animation-list.md](03-animation-list.md).

---

## Method 1 — RDR3 natives (direct)

The standard way to play any streamed animation in RedM:

```lua
local ped  = PlayerPedId()
local dict = 'redmorrow_com@pose5'
local clip = 'pose5'

-- 1. Request the dictionary
RequestAnimDict(dict)

-- 2. Wait until loaded
while not HasAnimDictLoaded(dict) do
    Wait(0)
end

-- 3. Play the animation
TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
```

### TaskPlayAnim parameters (RedM / RDR3)

RedM uses the **13-parameter** RDR3 version of `TaskPlayAnim`:

```lua
TaskPlayAnim(
    ped,        -- entity
    dict,       -- animation dictionary
    clip,       -- clip name inside the dictionary
    blendIn,    -- blend-in speed (e.g. 4.0)
    blendOut,   -- blend-out speed (e.g. -4.0)
    duration,   -- -1 = full clip length
    flags,      -- see flag table below
    startPhase, -- 0.0
    p8,         -- false
    ikFlags,    -- 0
    p10,        -- false
    taskFilter, -- 0
    p12         -- false
)
```

### Animation flags (RDR3)

RDR3 flag values **differ from GTA V**. Common values:

| Flag | Value | Effect |
| --- | ---: | --- |
| Loop | `1` | Repeats until stopped |
| Hold last frame | `2` | Plays once, freezes on final frame |
| Upper body | `8` | Plays on upper body only |
| Secondary | `16` | Runs alongside locomotion (combine with Upper body = `24`) |

**Examples:**

```lua
-- Loop (most poses in this pack default to loop)
TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)

-- Play once
TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, 0, 0.0, false, 0, false, 0, false)

-- Hold last frame
TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, 2, 0.0, false, 0, false, 0, false)

-- Upper body while walking (flag 8 + 16 = 24)
TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, 24, 0.0, false, 0, false, 0, false)
```

### Stop an animation

```lua
StopAnimTask(ped, dict, clip, 2.0)
-- or clear all tasks:
ClearPedTasks(ped, true, false)
```

### Check if playing

```lua
IsEntityPlayingAnim(ped, dict, clip, 3)
```

### Adjust playback speed

```lua
-- Native hash: _SET_ENTITY_ANIM_SPEED
Citizen.InvokeNative(0xEAA885BA3CEA4E4A, ped, dict, clip, 1.5) -- 1.5x speed
```

---

## Method 2 — Reusable client function

Drop this helper into any client script on your server:

```lua
local function PlayFemalePose(dict, clip, opts)
    opts = opts or {}
    local ped = PlayerPedId()
    local flags = opts.flags or 1  -- default: loop

    if not DoesAnimDictExist(dict) then
        print(('Dictionary "%s" not found — is rm_30-custom-female-pose started?'):format(dict))
        return false
    end

    RequestAnimDict(dict)
    local deadline = GetGameTimer() + 5000
    while not HasAnimDictLoaded(dict) do
        if GetGameTimer() > deadline then return false end
        Wait(0)
    end

    TaskPlayAnim(ped, dict, clip, 4.0, -4.0, -1, flags, 0.0, false, 0, false, 0, false)

    if opts.speed and opts.speed ~= 1.0 then
        Citizen.InvokeNative(0xEAA885BA3CEA4E4A, ped, dict, clip, opts.speed + 0.0)
    end

    return true
end

-- Usage:
PlayFemalePose('redmorrow_com@pose5', 'pose5')
PlayFemalePose('redmorrow_com@pose10', 'pose10', { flags = 2 })           -- hold
PlayFemalePose('redmorrow_com@pose8', 'pose8', { flags = 24 })          -- walk
PlayFemalePose('redmorrow_com@pose36', 'pose36', { flags = 1, speed = 0.5 })
```

---

## Method 3 — Integrate with an emote system

Add entries from `clips.lua` into your emote resource's animation table. The exact format depends on your emote system, but every system needs at minimum:

- **Dictionary** (`dict`) — the `.ycd` file name without extension
- **Clip** (`clip`) — the clip name inside that dictionary

### Example: generic emote table entry

```lua
{
    name     = 'Female Pose 5',
    command  = 'fpose5',
    dict     = 'redmorrow_com@pose5',
    clip     = 'pose5',
    flag     = 1,       -- loop
    duration = -1,
}
```

### Example: RM Emotes

If you use [RM Emotes](https://redmorrow.com/), add rows to your emote database or shared data with the `dict` and `clip` from [03-animation-list.md](03-animation-list.md). Set the animation type to a standard scripted anim and use flag `1` for loop poses.

Ensure `rm_30-custom-female-pose` starts **before or alongside** your emote resource so dictionaries are available when players open the menu.

### Example: command-based test

For quick server testing without an emote menu:

```lua
RegisterCommand('testpose', function(_, args)
    local id = args[1] or 'pose5'
    -- look up in Config.Clips from rm_30-custom-female-pose clips.lua
    PlayFemalePose('redmorrow_com@' .. id, id)
end, false)
```

---

## Method 4 — Read from clips.lua

The included `clips.lua` defines `Config.Clips` with every animation. You can reference it from another resource if you load the data manually, or copy entries into your own config.

Each entry contains:

| Field | Description |
| --- | --- |
| `id` | Short identifier (e.g. `pose5`) |
| `label` | Display name |
| `dict` | Animation dictionary |
| `clip` | Clip name inside the dictionary |
| `category` | Grouping label |
| `duration` | Length in seconds (reference only) |
| `mode` | Suggested mode: `once`, `loop`, or `hold` |
| `rootMotion` | Whether the clip moves the character |

Suggested flag from `mode`:

| mode | flag |
| --- | ---: |
| `once` | `0` |
| `loop` | `1` |
| `hold` | `2` |

---

## Important notes

1. **Do not rename `.ycd` files.** RDR2 dictionaries store their internal name; renaming breaks them.
2. **Do not change `dict` or `clip` in `clips.lua`** unless you know the exact names inside the `.ycd` file.
3. **Resource must be started** before any script requests these dictionaries.
4. **RedM only.** These are RDR2 `.ycd` files — they do not work on FiveM (GTA V).
5. **One dictionary per pose** in most cases. Exception: `pose29` uses dict `redmorrow_com@pose26` with clip `pose29`.

---

## Next steps

- Full animation table: [03-animation-list.md](03-animation-list.md)
- Edit labels and categories: [04-configuration.md](04-configuration.md)
- Something not working: [05-troubleshooting.md](05-troubleshooting.md)
