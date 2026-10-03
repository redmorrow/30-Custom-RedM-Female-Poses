# Installation

How to install the RM 30 Custom Female Pose Pack on a RedM server.

## 1. Requirements

| Requirement | Detail | Required |
| --- | --- | --- |
| RedM server | Any build supporting `fx_version 'cerulean'` and `lua54 'yes'` | Yes |
| Asset packs | Cfx.re asset entitlement (`dependency '/assetpacks'`) | Yes |
| Framework | VORP, RSG, RedEM:RP, or none | No |
| Database | oxmysql, MySQL, etc. | No |
| Emote system | RM Emotes, custom menu, or your own scripts | Optional |

**Not required:** npm, build tools, SQL imports, or any additional resources.

## 2. Folder placement

Place the resource anywhere your server loads resources from:

```
resources/[animations]/rm_30-custom-female-pose
resources/[standalone]/rm_30-custom-female-pose
```

**Keep the folder named `rm_30-custom-female-pose`.** Do not rename it. Other scripts and documentation reference this exact name.

Do not nest the folder inside another resource. Do not leave version suffixes such as `rm_30-custom-female-pose-1.0.0`.

Expected folder structure after install:

```
rm_30-custom-female-pose/
  fxmanifest.lua
  config.lua
  clips.lua
  stream/
    redmorrow_com@pose5.ycd
    redmorrow_com@pose6.ycd
    ... (one .ycd per dictionary)
  docs/
  README.md
  LICENSE.md
```

## 3. server.cfg

Add one line to your `server.cfg`:

```cfg
ensure rm_30-custom-female-pose
```

No specific order is required relative to frameworks. The resource has no server scripts and no database dependency.

Example standalone setup:

```cfg
ensure rm_30-custom-female-pose
```

Example with a framework:

```cfg
ensure vorp_core
ensure rm_emotes
ensure rm_30-custom-female-pose
```

## 4. First start

1. Save `server.cfg`.
2. Restart the server, or run in the server console:
   ```
   refresh
   ensure rm_30-custom-female-pose
   ```
3. Confirm the resource started without errors in the server console.

## 5. Verification checklist

Run through these checks after install:

| Step | How to verify | Expected result |
| --- | --- | --- |
| Resource started | Server console after `ensure` | No red errors for `rm_30-custom-female-pose` |
| Dictionary exists | F8 client console: `DoesAnimDictExist('redmorrow_com@pose5')` | Returns `1` (true) |
| Animation loads | Use the test snippet in [02-integration.md](02-integration.md) | Character plays the pose |
| Asset packs | If resource fails to start with asset error | Your server key needs Cfx.re asset pack entitlement |

### Quick in-game test

Paste this into any client script or run from a test command:

```lua
CreateThread(function()
    local dict, clip = 'redmorrow_com@pose5', 'pose5'
    RequestAnimDict(dict)
    local timeout = GetGameTimer() + 5000
    while not HasAnimDictLoaded(dict) do
        if GetGameTimer() > timeout then
            print('FAILED: dictionary did not load — is rm_30-custom-female-pose started?')
            return
        end
        Wait(0)
    end
    TaskPlayAnim(PlayerPedId(), dict, clip, 4.0, -4.0, -1, 1, 0.0, false, 0, false, 0, false)
    print('SUCCESS: pose5 is playing')
end)
```

## 6. Common install mistakes

| Mistake | Symptom | Fix |
| --- | --- | --- |
| Renamed folder | Other scripts cannot find animations | Rename back to `rm_30-custom-female-pose` |
| Forgot `ensure` | `DoesAnimDictExist` returns false | Add `ensure rm_30-custom-female-pose` to `server.cfg` |
| Resource not restarted | Old state, animations missing | `refresh` then `ensure rm_30-custom-female-pose` |
| Missing asset entitlement | Resource fails on asset pack check | Ensure your Cfx.re key has asset packs enabled |
| Renamed `.ycd` files | Dictionary loads but clip missing | Restore original file names — see [03-animation-list.md](03-animation-list.md) |
| Wrong game (FiveM) | Animations do not exist | This pack is RedM (RDR3) only |

## 7. Next steps

- Play poses with natives: [02-integration.md](02-integration.md)
- See all animation names: [03-animation-list.md](03-animation-list.md)
- Customize labels in `clips.lua`: [04-configuration.md](04-configuration.md)
