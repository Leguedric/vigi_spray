# vigi_spray - Developer Documentation

> **Author**: VigiLabs

**[Documentation](https://vigilabs.gitbook.io/vigilabs-docs)** | **[Discord Support](https://discord.gg/BntQVk5TqV)** | **[Tebex](https://vigilabs.tebex.io/package/vigi-spray)**

---

## Open Files (Non-Escrowed)

| File | Purpose |
|---|---|
| `config.lua` | All configurable settings |
| `client/bridge.lua` | Client-side framework bridge (ESX / QBCore / ox_core) |
| `server/bridge.lua` | Server-side framework & inventory bridge |
| `locales/*.lua` | Translation files |

---

## Configuration (`config.lua`)

### Framework & Inventory

```lua
Config.Framework = "auto"           -- "auto", "esx", "qbcore", "oxcore"
Config.Inventory = "auto"           -- "auto", "qs", "qb", "ox", "codem", "esx", "chezza", "none"
```

Both support auto-detection. Set manually only if detection fails.

> **ox_core**: no extra dependency is required. The bridge talks to ox_core through
> its `GetPlayer` / `CallPlayer` exports, so you do **not** need to add anything to
> `fxmanifest.lua`. ox_core has no inventory of its own, pair it with `ox_inventory`.

### Items

```lua
Config.Items = {
    sprayCan = "spraycan",          -- Item name in your database
    sponge   = "sponge"
}
```

> These must match exactly your items table (e.g. in `items.lua` or your database).

#### ox_inventory item declaration

Declare the items plainly, with **no `consume`, `usetime`, `status` or `export`**:

```lua
['spraycan'] = { label = 'Spray Can', weight = 500 },
['sponge']   = { label = 'Sponge',    weight = 200 },
```

No `export` line is needed — vigi_spray listens to `ox_inventory:usedItem`.

> Adding `usetime`, `status` or `export` makes ox_inventory set `consume = 1`, and
> the spray can is then removed **twice**: once by ox_inventory and once by
> `Config.ConsumeItem`. If you want a use animation, set `consume = 0` explicitly.

### Storage (JSON or MySQL)

```lua
Config.Storage = {
    mode        = "json",   -- "json" (default, flat files) or "mysql"
    autoMigrate = true,     -- Auto-import existing .json files on first MySQL boot
}
```

- **`"json"`** - default, no setup. Data lives in `tags.json`, `stencils.json`, `bans.json`.
- **`"mysql"`** - requires `oxmysql` or `mysql-async`. Schema is created automatically (no SQL import). First boot auto-migrates existing JSON data if any, renaming files to `.migrated` as backup.

Graffiti images (`.webp`) always stay on disk under `data/tags/` and `data/stencils/`, regardless of the backend. Both folders are created automatically when the resource starts, and recreated if they go missing - deleting them loses every graffiti image.

> See the [full Storage guide](https://vigilabs.gitbook.io/vigilabs-docs) for setup, migration, rollback, schema and backups.

### Props (Spray Can & Sponge)

```lua
Config.Prop = {
    model = 'prop_cs_spray_can',
    bone = 57005,
    pos = vector3(0.077, -0.006, -0.075),
    rot = vector3(-31.5, 83.5, 53.5)
}

Config.Sponge = {
    model = "prop_sponge_01",
    bone = 28422,
    idle = { pos = vector3(...), rot = vector3(...) },
    scrub = { pos = vector3(...), rot = vector3(...) }
}
```

### Spray Mechanics

```lua
Config.SprayDistance = 10.0         -- Raycast range
Config.Spray.MaxDistance = 7.0      -- Max wall distance while spraying
Config.Spray.MinSize = 0.01         -- Min cap size
Config.Spray.MaxSize = 0.10         -- Max cap size
Config.Spray.SizeStep = 0.005       -- Size change per scroll
```

### Pressure System

```lua
Config.Pressure = {
    maxPressure = 100.0,
    pressurePerShake = 80.0,
    pressureDecayRate = 2.0,
    minPressureForSpray = 5.0,
    sputteringThreshold = 20.0,
    lowPressureOpacity = 0.3,
    lowPressureSize = 0.5
}
```

### Cleaning & Sponge Durability

```lua
Config.Cleaning = {
    eraseStrength = 0.35,           -- 0.1 (slow) to 1.0 (instant)
    eraserSize = 20,                -- Eraser radius in DUI pixels
    cleaningDistance = 2.0,         -- Max cleaning range (meters)
    durabilitySystem = true,        -- If true, the sponge degrades and eventually breaks
    maxDurability = 100.0,          -- Starting durability pool
    durabilityLossPerTick = 0.1     -- How much is lost while actively scrubbing
}

Config.Sponge = {
    model = "prop_sponge_01",
    bone = 28422,
    idle = { pos = vector3(...), rot = vector3(...) },
    scrub = { pos = vector3(...), rot = vector3(...) }
}

```

> **Premium UI**: When `durabilitySystem` is enabled, a dynamic circular arc appears around the cleaning cursor, changing from Cyan ➔ Orange ➔ Red as the sponge wears out. Once depleted, the item is removed from the player's inventory.

### Rendering

```lua
Config.MaxDrawDistance = 100.0          -- Tags visible up to this distance
Config.MaxActiveTags = 32               -- Max simultaneous rendered tags (atlas slots)
Config.TagExpirationDays = 180          -- Auto-delete after N days (0 = never)
```

### Audio

```lua
Config.Audio = {
    hearingRange = 15.0  -- Max distance to hear shake/erase sounds
}
```

### Gameplay

```lua
Config.ConsumeItem = true  -- Removes 1 spray can after painting (set false for infinite)

### Command Fallback

Useful for unsupported inventories or custom setups where items cannot be registered.

```lua
Config.UseCommands = true            -- Enable /spray and /sponge
Config.Commands = {
    spray = "spray",
    sponge = "sponge"
}
```

> **Note:** When enabled, players can use `/spray` to start spraying and `/sponge` to start cleaning without needing to use an item from their inventory. If an inventory IS detected, the script will still check if the player has the required item (unless `Config.Inventory` is set to `"none"`).
```

### Admin

```lua
Config.AdminCommand = "graffadmin"  -- Chat command to open admin panel
```

### Permissions

The script features a powerful, unified permission system that allows you to restrict graffiti placement based on several criteria. **All checks are performed server-side.**

```lua
Config.Permission = {
    enabled = true,                          -- Master switch: must be true to enable any check
    acePermission = "vigi_spray.use",        -- ACE permission (FiveM native groups)
    bossOnly = false,                        -- ONLY job bosses (ESX grade 'boss', QB isboss, ox_core boss permission or grade name)
    bossGradeNames = {"boss"},               -- [ESX / ox_core] List of grade names considered as "boss" (e.g. {"boss", "ceo"})
    allowedJobs = {},                        -- Job whitelist, e.g. {"police", "ballas"}
    allowedRoles = {}                        -- Discord Role IDs, e.g. {"1234567890"}
}
```

#### 1. ACE Permissions (FiveM Native)
Grant access to a specific group or identifier in your `server.cfg`:

```bash
# Grant access to a group
add_ace group.vip vigi_spray.use allow
# Link a player to that group
add_principal identifier.discord:1122334455667788 group.vip
```

#### 2. Job & Boss Control (ESX / QBCore / ox_core)
- **`bossOnly`**: Automatically detects if the player is a leader in their current framework.
- **`bossGradeNames`**: For ESX and ox_core, you can specify multiple grade names that are considered "bosses" (e.g., if some jobs use `"boss"` while others use `"ceo"` or `"director"`).

> **ox_core has groups, not jobs.** `allowedJobs` is matched against **group names**,
> and simply belonging to the group is enough — it does not have to be the active one,
> since a character can hold several groups at once.
>
> For `bossOnly`, ox_core is checked in two steps: first the `group.<name>.boss`
> permission if your server defines one, then the grade label against `bossGradeNames`.

#### 3. External Export Check
You can link **any other resource** to handle permission checks. This is ideal if you have a custom gang territory system or a unique permission script.

```lua
Config.ExternalCheck = {
    enabled = true,                        -- Enable the external check
    exportResource = "my_gang_script",     -- Name of the external resource
    exportName = "canPlayerSpray"          -- Function name: function(playerSource)
}
```

The external script must define the export like this:
```lua
-- In 'my_gang_script' server-side
exports('canPlayerSpray', function(source)
    -- Your custom logic (e.g. check territory, item, etc.)
    if playerIsAllowed then
        return true
    else
        return false -- Block painting/cleaning
    end
end)
```

- **`allowedJobs`**: Only players in the specified jobs can use the spray can.

#### 3. Discord Roles
To use **`allowedRoles`**, you must link the script to your Discord bridge (e.g., BadgerDiscordAPI).
1. Add the Role IDs to `Config.Permission.allowedRoles`.
2. Edit **`server/bridge.lua`** and customize the **`Bridge.HasDiscordRole`** function with your specific bridge export.

#### 4. Admin Blacklist (UI)
Regardless of permissions, any player added to the **Blacklist** via the Admin Panel (`/graffadmin`) is permanently blocked from spraying until removed by an admin.

### Restricted Zones

Define polygon areas where graffiti is forbidden. Uses 2D point-in-polygon check (ignores Z-axis, covers full building height).

```lua
Config.RestrictedZones = {
    enabled = true,
    zones = {
        {
            name = "Police Station",        -- Zone name (shown in notification)
            points = {                      -- Polygon vertices (auto-closes first↔last)
                vector3(186.26, -840.62, 30.91),
                vector3(127.10, -988.16, 29.28),
                vector3(213.61, -1020.38, 29.31),
                vector3(266.20, -870.31, 29.11),
            }
        },
    }
}
```

> **Tip:** Minimum 3 points per zone. The polygon auto-closes (first point connects to last).

---

### Admin Bulk Actions

The admin panel now includes a "Premium" bulk delete system:
1. **Selection**: Select multiple graffiti tags using the checkboxes in the first column.
2. **Select All**: Use the header checkbox to select all tags on the current page.
3. **Action Bar**: A floating action bar appears at the bottom once tags are selected.
4. **Optimized Deletion**: Clicking "Delete Selected" performs a batch deletion on the server, cleaning up all selected tags and their PNG files in a single optimized pass.

### OP Gangs Integration (op-crime)

Native integration with [OP Gangs](https://otherplanet.dev/) - uses the official `op-crime` graffiti events. All loyalty, XP and turf configuration is handled automatically by op-crime's own config.

```lua
Config.OPGangs = {
    enabled = true              -- Enable OP Gangs integration
}
```

**How it works:**
- When a player **paints** a graffiti → `op-crime:onGraffitiPaint` is triggered server-side
- When a player **cleans** a graffiti → `op-crime:onGraffitiRemove` is triggered server-side
- op-crime automatically handles turf detection, loyalty rewards, rival penalties, and organisation XP

> **No additional configuration required.** Loyalty values, XP amounts, and turf rules are managed in op-crime's own config file.

### Discord Webhook

```lua
Config.Discord = {
    Webhook = "https://discord.com/api/webhooks/...",
    Color = 3447003,
    Author = {
        Name = "Vigi Spray LOGS",
        Icon = "https://..."
    }
}
```

### Debug

```lua
Config.Debug = false  -- Enables verbose console output + /graffitidebug command
```

---

## Exports

### Client-Side

#### `IsSprayMode()`

Returns `true` if the local player is currently in spray or cleaning mode.

```lua
local isBusy = exports['vigi_spray']:IsSprayMode()
if isBusy then
    -- Block inventory opening, etc.
end
```

#### `OpenAdminPanel()`

Opens the graffiti admin panel (server-side permission check is included automatically).

```lua
-- From your custom admin menu
exports['vigi_spray']:OpenAdminPanel()
```

#### `OpenStencilGallery()`

Opens the stencil gallery for the player to select a design.

```lua
-- From a custom interaction menu or keybind
exports['vigi_spray']:OpenStencilGallery()
```

#### `GetNearbyTags(radius)` *(Client-Side)*

Returns a table of nearby tags (within loaded range) around the player.

```lua
local tags = exports['vigi_spray']:GetNearbyTags(50.0)
for _, tag in ipairs(tags) do
    if tag.stencilId then
        print("Stencil tag found! Stencil ID: " .. tag.stencilId)
    end
end
```

**Returned fields per tag:**

| Field | Type | Description |
|---|---|---|
| `id` | `string` | UUID of the tag |
| `coords` | `vector3` | Position of the tag |
| `stencilId` | `string?` | Stencil ID used (`nil` if hand-drawn) |
| `distance` | `number` | Distance from the player |

#### `SetGraffitiHidden(hidden)`

Hides or shows all graffiti rendering. Use this when opening a UI that uses blur (inventory, phone, etc.) since FiveM's `DrawSpritePoly` ignores NUI blur effects.

```lua
-- When opening your inventory
exports['vigi_spray']:SetGraffitiHidden(true)

-- When closing your inventory
exports['vigi_spray']:SetGraffitiHidden(false)
```

#### `IsGraffitiHidden()`

Returns `true` if graffiti is currently hidden.

```lua
local hidden = exports['vigi_spray']:IsGraffitiHidden()
```

#### `StartCustomCleaning(options)`

Enters cleaning mode **without consuming a sponge**. Use this to integrate the Vigi Spray cleaning UI (cyan reticle, lock detection, persistence to disk) with custom in-game tools - pressure washer, fire-truck hose, magic wand, etc.

```lua
local ok = exports['vigi_spray']:StartCustomCleaning({
    eraserSize       = 60,    -- cursor radius in DUI pixels (optional, default Config.Cleaning.eraserSize)
    cleaningDistance = 12.0,  -- max reach in meters (optional, default Config.Cleaning.cleaningDistance)
    useProp          = false, -- attach a prop + play scrub anim? (optional, default false)
    propConfig       = nil,   -- if useProp = true, custom prop table - same shape as Config.Sponge
    confirmKey       = 24,    -- GTA V control ID to hold for cleaning (optional, default Config.Keys.Confirm = LMB)
    cancelKey        = 177,   -- GTA V control ID to press to exit (optional, default Config.Keys.Cancel = Backspace)
})
```

Returns `true` if the cleaning session started, `false` if the player was already in another spray/cleaning session.

When `useProp = false` (the default) **no prop is attached and no animation is played** - the calling resource is expected to handle visuals (its own attached prop, particle effects, water spray, etc.).

The server still validates proximity and lock state. To allow long-range tools, raise `Config.Cleaning.maxRemoteDistance` server-side. When unset, the server caps cleaning at `cleaningDistance + 5m` regardless of what the export passes.

#### `StopCleaning()`

Forces the active cleaning session (sponge **or** custom) to exit. No-op when the player isn't currently cleaning.

```lua
exports['vigi_spray']:StopCleaning()
```

---

### Server-Side

#### `DeleteTag(tagId)`

Deletes a specific graffiti tag by its UUID. Returns `true` if deleted, `false` if not found.

```lua
local success = exports['vigi_spray']:DeleteTag("a1b2c3d4-...")
if success then
    print("Tag deleted")
end
```

#### `DeleteClosestTag(coords, radius)`

Deletes the single closest graffiti tag within `radius` meters of `coords`. Returns `true` if a tag was deleted, `false` otherwise. Useful for automated cleanup (e.g., rival territory scripts).

```lua
local coords = GetEntityCoords(GetPlayerPed(source))
local deleted = exports['vigi_spray']:DeleteClosestTag(coords, 5.0)
if deleted then
    print("Closest tag removed!")
end
```

#### `GetNearbyTags(coords, radius)` *(Server-Side)*

Returns a table of tags within `radius` meters of `coords`.

```lua
local tags = exports['vigi_spray']:GetNearbyTags(vector3(100.0, 200.0, 30.0), 50.0)
for _, tag in ipairs(tags) do
    print(tag.id, tag.creatorName, tag.stencilId or "hand-drawn")
end
```

**Returned fields per tag:**

| Field | Type | Description |
|---|---|---|
| `id` | `string` | UUID of the tag |
| `coords` | `vector3` | Position of the tag (point A) |
| `creatorName` | `string` | In-game name of the creator |
| `discordId` | `string` | Discord identifier of the creator |
| `stencilId` | `string?` | Stencil ID used (`nil` if hand-drawn) |
| `time` | `number` | Unix timestamp of creation |

#### `GetTagInfo(tagId)`

Returns full metadata for a specific tag by its UUID. Returns `nil` if not found.

```lua
local info = exports['vigi_spray']:GetTagInfo("a1b2c3d4-...")
if info then
    print(info.creatorName, info.stencilId or "hand-drawn")
end
```

**Returned fields:**

| Field | Type | Description |
|---|---|---|
| `id` | `string` | UUID of the tag |
| `coords` | `vector3` | Position (point A) |
| `pA`, `pB` | `vector3` | Corner points |
| `normal` | `vector3` | Surface normal |
| `creatorName` | `string` | Creator's RP name |
| `discordId` | `string` | Creator's Discord ID |
| `stencilId` | `string?` | Stencil ID (`nil` if hand-drawn) |
| `time` | `number` | Unix timestamp |
| `hasSprayed` | `boolean` | Whether the tag has content |

#### `IsStencilTag(tagId)`

Quick check - returns the `stencilId` if the tag was made from a stencil, `false` otherwise.

```lua
local stencil = exports['vigi_spray']:IsStencilTag("a1b2c3d4-...")
if stencil then
    print("This tag uses stencil: " .. stencil)
end
```

#### `GetAllStencils()`

Returns a table of all available stencils with their ID and name. Useful for discovering stencil IDs programmatically.

```lua
local stencils = exports['vigi_spray']:GetAllStencils()
for _, s in ipairs(stencils) do
    print(s.id, s.name)  -- e.g. "13558a5f-...", "Ballas Logo"
end
```

**Returned fields per stencil:**

| Field | Type | Description |
|---|---|---|
| `id` | `string` | UUID of the stencil |
| `name` | `string` | Name of the stencil |

> **Tip:** You can also click on a stencil's ID in the admin panel (Stencils tab) to copy it to your clipboard.

#### Server Events

Want to react immediately when a tag is placed or cleaned? Listen to these server events from any external script:

**`vigi_spray:server:onTagCreated`**
```lua
AddEventHandler('vigi_spray:server:onTagCreated', function(source, tagId, tagData, opGangsTurf)
    print("Player " .. source .. " just created tag " .. tagId)
    -- tagData contains: pA, pB, normal, creatorName, discordId, stencilId, time, gangId
    -- opGangsTurf contains the Turf Zone index if op-crime is used
end)
```

**`vigi_spray:server:onTagCleaned`**
```lua
AddEventHandler('vigi_spray:server:onTagCleaned', function(source, tagId, tagData, opGangsTurf)
    print("Player " .. source .. " fully cleaned tag " .. tagId)
    -- This only triggers when the spray is 100% erased (not just partially wiped)
end)
```

---

## Integration Example: Gang Territory

Use the exports to detect gang-specific stencils near a player:

```lua
-- Server-side
local GANG_STENCILS = {
    ["13558a5f-c5b9-..."] = "ballas",
    ["7f4be082-1a2b-..."] = "vagos"
}

local tags = exports['vigi_spray']:GetNearbyTags(playerCoords, 100.0)
for _, tag in ipairs(tags) do
    local gang = GANG_STENCILS[tag.stencilId]
    if gang then
        print("Player is in " .. gang .. " territory!")
    end
end
```

---

## Locales

Add or edit translation files in `locales/`. Create a file named `locales/xx.lua` (e.g., `locales/en.lua`) and set `Config.Locale = 'xx'`.

See `locales/en.lua` for the full list of required keys.

---

## Bridge Customization

Both `client/bridge.lua` and `server/bridge.lua` are open for modification. If you use a custom framework, you can adapt these files without touching the core code.

### Key functions to implement:

**Client** (`client/bridge.lua`):
- `Bridge.Initialize()` - Player loaded event
- `Bridge.GetPlayerData()` - Return player data object
- `Bridge.GetJobName()` - Return current job name
- `Bridge.HasItem(item, count)` - Does the player carry this item?
- `Bridge.TriggerCallback(name, cb, ...)` - Server callback trigger
- `Bridge.ShowNotification(msg, type)` - Display notification

**Server** (`server/bridge.lua`):
- `Bridge.OnPlayerLoaded(handler)` - Register player load handler
- `Bridge.RegisterCallback(name, handler)` - Register server callback
- `Bridge.GetUser(source)` - Get player object
- `Bridge.GetIdentifier(source)` - Get player identifier
- `Bridge.GetName(source)` - Get player RP name
- `Bridge.GetDiscordId(source)` - Get Discord identifier
- `Bridge.IsAdmin(source)` - Check admin permissions
- `Bridge.GetJob(source)` - Get the current job/group table
- `Bridge.HasJob(source, jobNames)` - Does the player hold any of these jobs/groups?
- `Bridge.IsBoss(source)` - Is the player a boss of their job/group?
- `Bridge.HasDiscordRole(source, roles)` - Discord role check (stub, customise it)
- `Bridge.RegisterUsableItem(item, handler)` - Register usable item
- `Bridge.RemoveItem(source, item, count)` - Remove item from inventory
- `Bridge.HasItem(source, item, count)` - Does the player carry this item?
