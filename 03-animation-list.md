# Animation List

Complete reference for all poses in the RM 30 Custom Female Pose Pack.

**Total animations:** 29  
**Format:** RDR2 `.ycd` (RSC8 v58)  
**Dictionary naming:** `redmorrow_com@<name>.ycd` → dict `redmorrow_com@<name>`

---

## All poses

| # | ID | Label | Dictionary | Clip | Duration | Suggested mode |
| ---: | --- | --- | --- | --- | ---: | --- |
| 1 | `lean` | lean | `redmorrow_com@lean` | `lean` | 1.967 s | loop |
| 2 | `pose5` | pose5 | `redmorrow_com@pose5` | `pose5` | 1.967 s | loop |
| 3 | `pose6` | pose6 | `redmorrow_com@pose6` | `pose6` | 1.967 s | loop |
| 4 | `hatsdown_clip` | hatsdown_clip | `redmorrow_com@pose7` | `hatsdown_clip` | 1.967 s | loop |
| 5 | `pose8` | pose8 | `redmorrow_com@pose8` | `pose8` | 1.967 s | loop |
| 6 | `pose10` | pose10 | `redmorrow_com@pose10` | `pose10` | 89 s | loop |
| 7 | `pose11` | pose11 | `redmorrow_com@pose11` | `pose11` | 89 s | loop |
| 8 | `pose13` | pose13 | `redmorrow_com@pose13` | `pose13` | 89 s | loop |
| 9 | `pose17` | pose17 | `redmorrow_com@pose17` | `pose17` | 89 s | loop |
| 10 | `pose18` | pose18 | `redmorrow_com@pose18` | `pose18` | 89 s | loop |
| 11 | `pose23` | pose23 | `redmorrow_com@pose23` | `pose23` | 0.1 s | loop |
| 12 | `pose29` | pose29 | `redmorrow_com@pose26` | `pose29` | 3.7 s | loop |
| 13 | `pose31` | pose31 | `redmorrow_com@pose31` | `pose31` | 3.7 s | loop |
| 14 | `pose32` | pose32 | `redmorrow_com@pose32` | `pose32` | 3.7 s | loop |
| 15 | `pose33` | pose33 | `redmorrow_com@pose33` | `pose33` | 3.7 s | loop |
| 16 | `pose36` | pose36 | `redmorrow_com@pose36` | `pose36` | 9 s | loop |
| 17 | `pose41` | pose41 | `redmorrow_com@pose41` | `pose41` | 9 s | loop |
| 18 | `pose42` | pose42 | `redmorrow_com@pose42` | `pose42` | 9 s | loop |
| 19 | `pose44` | pose44 | `redmorrow_com@pose44` | `pose44` | 9 s | loop |
| 20 | `pose49` | pose49 | `redmorrow_com@pose49` | `pose49` | 9 s | loop |
| 21 | `pose51` | pose51 | `redmorrow_com@pose51` | `pose51` | 9 s | loop |
| 22 | `pose52` | pose52 | `redmorrow_com@pose52` | `pose52` | 9 s | loop |
| 23 | `pose55` | pose55 | `redmorrow_com@pose55` | `pose55` | 9 s | loop |
| 24 | `pose56` | pose56 | `redmorrow_com@pose56` | `pose56` | 1 s | loop |
| 25 | `pose57` | pose57 | `redmorrow_com@pose57` | `pose57` | 1 s | loop |
| 26 | `pose58` | pose58 | `redmorrow_com@pose58` | `pose58` | 1 s | loop |
| 27 | `pose59` | pose59 | `redmorrow_com@pose59` | `pose59` | 1 s | loop |
| 28 | `pos60` | pos60 | `redmorrow_com@pos60` | `pos60` | 1 s | loop |
| 29 | `pose65` | pose65 | `redmorrow_com@pose65` | `pose65` | 1.967 s | loop |

---

## Stream files

Each dictionary requires one `.ycd` file in `stream/`:

```
stream/redmorrow_com@lean.ycd
stream/redmorrow_com@pose5.ycd
stream/redmorrow_com@pose6.ycd
stream/redmorrow_com@pose7.ycd
stream/redmorrow_com@pose8.ycd
stream/redmorrow_com@pose10.ycd
stream/redmorrow_com@pose11.ycd
stream/redmorrow_com@pose13.ycd
stream/redmorrow_com@pose17.ycd
stream/redmorrow_com@pose18.ycd
stream/redmorrow_com@pose23.ycd
stream/redmorrow_com@pose26.ycd
stream/redmorrow_com@pose31.ycd
stream/redmorrow_com@pose32.ycd
stream/redmorrow_com@pose33.ycd
stream/redmorrow_com@pose36.ycd
stream/redmorrow_com@pose41.ycd
stream/redmorrow_com@pose42.ycd
stream/redmorrow_com@pose44.ycd
stream/redmorrow_com@pose49.ycd
stream/redmorrow_com@pose51.ycd
stream/redmorrow_com@pose52.ycd
stream/redmorrow_com@pose55.ycd
stream/redmorrow_com@pose56.ycd
stream/redmorrow_com@pose57.ycd
stream/redmorrow_com@pose58.ycd
stream/redmorrow_com@pose59.ycd
stream/redmorrow_com@pos60.ycd
stream/redmorrow_com@pose65.ycd
```

**Note:** `pose29` shares the `redmorrow_com@pose26.ycd` dictionary but uses clip name `pose29`.

---

## Quick copy — native examples

```lua
-- pose5
TaskPlayAnim(ped, 'redmorrow_com@pose5', 'pose5', 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)

-- hatsdown_clip (pose7 dictionary)
TaskPlayAnim(ped, 'redmorrow_com@pose7', 'hatsdown_clip', 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)

-- pose29 (pose26 dictionary)
TaskPlayAnim(ped, 'redmorrow_com@pose26', 'pose29', 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)

-- pos60
TaskPlayAnim(ped, 'redmorrow_com@pos60', 'pos60', 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
```

---

## Editing labels

You may rename `label` and `category` in `clips.lua` for your emote system. Never change `dict` or `clip` unless you verify the exact names inside the `.ycd` file.

See [04-configuration.md](04-configuration.md).
