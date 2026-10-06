## Transform your streets into a living canvas

**Vigi Spray** is the **most advanced, high-performance graffiti system** available for FiveM. Players can freehand paint on any wall, mask areas with professional tape, use stencils from a gallery or URL, mirror their strokes, and express their creativity in real-time -- all synced live to every player nearby.

Packed with a fully integrated admin dashboard, layered permission systems, real-time syncing, and extreme performance. This is the ultimate tool for gangs, street artists, and law enforcement roleplay.

> **New in v1.9.0** -- Vigi Spray now runs on **ox_core**, alongside ESX, QBCore and Qbox. Auto-detected, with no extra dependency and nothing to add to your `fxmanifest.lua`.

![VigiSpray|600x337, 100%](upload://swww6swjIYjqGdxtnHGTDd5JIVa.gif)

---

## Showcase

**Core Features Trailer:**

https://www.youtube.com/watch?v=wDyEfsdmUMw

**Stencil System Update:**

https://www.youtube.com/watch?v=DZG23vJ4SFc

**Professional Masking Tape Update:**

https://www.youtube.com/watch?v=VrI-_7iDG84

[grid]
![Work area with dimensions|690x388](upload://9kruDmDavVAm2YcgoGjN6JIWN0p.jpeg)
![Hand-painted graffiti using masking tape after|690x388](upload://7IRZHJBODKrKKB6O5c5ZFWpnh1F.jpeg)
![Hand-painted graffiti using masking tape|690x388](upload://jyL58Qn31Nu9hPSFYVaYT8PRlmD.jpeg)
![Selecting a predefined stencil|690x388](upload://1C1ee51v2M2fQsFpWI6Ylp8r1Lg.jpeg)
[/grid]

---

## Features

### Freehand Spray Painting

- Paint on **any flat surface** in the world with full mouse control.
- **LIVE Syncing** -- watch other players spray and draw in real-time.
- **Color Picker** with presets, recent colors, and favorites (right-click to save).
- **Pressure System** -- shake the can to build pressure, watch it sputter when running low.
- **Adjustable Cap Size** -- scroll to change stroke width from thin to fat cap.

### Professional Masking Tape

- Outline clean straight lines and perfect geometric shapes.
- **Angle Snapping** (hold SHIFT) for precise 45-degree alignments.
- **Dynamic 3D Dimensions** displayed while placing your work area.
- **Rule of Thirds Grid** overlay to help players scale and compose their art.

### Mirror Mode

- Place a **symmetry axis** anywhere on the canvas.
- Every stroke is automatically reflected across the axis in real-time.
- Angle snapping supported for axis placement.
- Create perfectly symmetrical designs with half the effort.

### Depth Adjustment

- Scroll to move the graffiti closer or further from the wall surface.
- Fixes Z-fighting on uneven or curved surfaces.
- Available to both players (own tags) and admins (any tag).

### Edit Mode

- Players can **re-edit their own graffiti** at any time.
- The canvas reopens with the existing artwork loaded.
- Continue drawing, add details, fix mistakes, or erase sections.
- Admins can **lock** tags to prevent editing and cleaning.

### Stencil Gallery & URL Import

- **In-Game Stencil Gallery** -- browse and select pre-defined high-res designs.
- **Dynamic Reveal Animation** -- watch the stencil appear progressively as you spray.
- **Player Access Control** -- restrict specific stencils to specific players.
- **Player URL Import** (optional) -- paste a URL (Imgur, Discord CDN, etc.) to paint any image, with configurable domain whitelist/blacklist and cooldowns.

### Local Sketchbook

- Players can **save drawings locally** and reuse them across sessions.
- Personal library stored client-side -- no server storage needed.
- Load a saved sketch onto any new canvas instantly.

### Immersive Cleaning

- **Sponge Cleaning** -- scrub away graffiti progressively with a physical sponge animation.
- **Durability System** -- sponges degrade over time with a real-time wear indicator (cyan > orange > red).
- When the sponge breaks, it is removed from the player's inventory.

---

## Admin Panel

The most complete graffiti admin panel available for FiveM.

- **Interactive World Map** -- Leaflet.js map with clustering. Switch between Atlas, Satellite, and Roads views.
- **Dashboard** -- total graffiti count, active artists, daily stats.
- **Search, Filter & Sort** -- find tags by artist name, ID, date, or distance from your position.
- **Bulk Delete** -- select multiple tags and delete them in a single optimized batch.
- **Click-to-Delete Tool** -- enter a special mode to aim and click to remove tags directly in-game.
- **Admin Depth Adjustment** -- aim at any tag and scroll to fine-tune its wall offset.
- **Tag Locking** -- lock any tag to prevent players from editing or cleaning it.
- **Stencil Library Management** -- add, rename, import, delete, and control player access for stencils.
- **Blacklist System** -- ban/unban players from using spray cans via Discord ID, License, or Server ID. Fully in-game UI.
- **Discord Webhook Logs** -- every tag creation is logged with artist info, coordinates, and an image preview.

[grid]
![Dashboard with all the server graffiti|690x376](upload://3EWUvN9tbFfOsG03qWy8UgOk50P.jpeg)
![Selection of a graffiti|690x380](upload://fUXpqj60lphUhNoVRWHDalkzLfL.jpeg)
![Stencils|690x388](upload://fF69YzsE0MX4PD4E22vH87c3Cir.jpeg)
![Map with all Graffiti|690x377](upload://5pemvPkKItlGig4oldlaDPJrRj8.jpeg)
![Teleport on a graffiti ou delete|690x384](upload://jZS9gh7uPIaGlgCZtISgrRSPgIU.jpeg)
![Ban a player from using graffiti|690x378](upload://ihel0EKlMQueRJTu7LmOOOIiADD.jpeg)
[/grid]

---

## Performance

Vigi Spray is built for servers with hundreds of tags and dozens of concurrent players.

- **Atlas Rendering Engine** -- all visible tags are rendered via a single optimized GPU texture atlas. Hundreds of graffiti, minimal FPS impact.
- **Camera-Side Face Culling** -- only the face visible to the player is rendered (2 draw calls instead of 4). Backface only renders within 15m.
- **Debounced File I/O** -- rapid operations (edits, depth changes, stencil placements) are batched to reduce disk writes.
- **Latent Event Streaming** -- large images and stencils are synced via chunked latent events. No network bottleneck.
- **WebP Compression** -- all artwork is stored in WebP format for optimal quality-to-size ratio.
- **Data Integrity Check** -- automatic cleanup of orphaned files and entries on server start.
- **Zero External Dependencies** -- no xSound or external libraries. Spatial audio is built entirely within NUI.

---

## Framework Support

One script, four frameworks. **ESX**, **QBCore**, **Qbox** and **ox_core** are all auto-detected, so you drop the resource in and it works.

- **No extra dependency for ox_core** -- nothing to add to your `fxmanifest.lua`. The bridge talks to ox_core directly through its own exports.
- **ox_core groups are handled the way ox_core actually works** -- it has groups rather than jobs, and a character can hold several at once, so job whitelists match on group membership. It does not have to be your active group.
- **Both bridge files stay open** (`client/bridge.lua`, `server/bridge.lua`). Running a custom or heavily modified framework? Adapt them without ever touching the core code.

> ox_core has no inventory of its own. Pair it with **ox_inventory** (declare `spraycan` and `sponge` plainly, no `export` line needed), or use the command-only mode.

---

## Permissions & Restrictions

A layered, server-side permission system:

- **ACE Permissions** -- restrict spraying to specific FiveM groups.
- **Job & Boss Grade** -- allow only specific jobs or boss ranks (ESX grade names, QB `isboss`, ox_core group grades and permissions).
- **Discord Role Check** -- restrict to specific Discord roles (requires a Discord bridge).
- **External Export** -- hook into any custom resource with a simple `true/false` export.
- **Restricted Zones** -- define polygon areas where graffiti is forbidden (e.g., police station, hospital).
- **Player Blacklist** -- permanently block players via the admin panel.

All checks stack. Combine ACE + Job + Discord + Zones for full control.

---

## Integrations

- **OP Gangs (op-crime)** -- native integration. Painting triggers `onGraffitiPaint`, cleaning triggers `onGraffitiRemove`. Turf detection, loyalty rewards, and rival penalties handled automatically by op-crime.
- **Any Custom System** -- use server events and exports to integrate with police alerts, gang territory scripts, economy systems, and more.

---

## API for Developers

Vigi Spray exposes a full API for building on top of the graffiti system.

**Server Events (triggered automatically):**

```lua
AddEventHandler('vigi_spray:server:onTagCreated', function(source, tagId, tagData, turfIndex)
    -- React when a tag is placed (tagData contains coords, artist, stencilId, gangId...)
end)

AddEventHandler('vigi_spray:server:onTagCleaned', function(source, tagId, tagData, turfIndex)
    -- React when a tag is fully scrubbed away
end)
```

**Server Exports:**

```lua
exports['vigi_spray']:DeleteTag(tagId)              -- Delete a tag by UUID
exports['vigi_spray']:DeleteClosestTag(coords, r)   -- Delete nearest tag within radius
exports['vigi_spray']:GetNearbyTags(coords, radius)  -- Get all tags in range
exports['vigi_spray']:GetTagInfo(tagId)              -- Full tag metadata
exports['vigi_spray']:IsStencilTag(tagId)            -- Check if tag uses a stencil
exports['vigi_spray']:GetAllStencils()               -- List all stencils
```

**Client Exports:**

```lua
exports['vigi_spray']:IsSprayMode()                  -- Is the player currently spraying?
exports['vigi_spray']:GetNearbyTags(radius)           -- Nearby tags around the player
exports['vigi_spray']:SetGraffitiHidden(bool)         -- Hide/show all graffiti rendering
exports['vigi_spray']:IsGraffitiHidden()              -- Check if graffiti is hidden
exports['vigi_spray']:OpenAdminPanel()                -- Open admin panel from your own menu
exports['vigi_spray']:OpenStencilGallery()            -- Open stencil gallery from your own menu
```

---

## Configuration

Everything is configurable via a single `config.lua`:

- **Framework & Inventory** -- auto-detects ESX, QBCore, Qbox, or ox_core. Supports OX, QS, QB, Codem, Chezza inventories, or command-only mode.
- Item names, prop models, and bone attachments.
- Spray distance, brush sizes, pressure decay, and cooldowns.
- Cleaning speed, eraser size, and sponge durability.
- Rendering distance, atlas slots, slot resolution, and WebP quality.
- Discord Webhooks with image embeds.
- Tag auto-expiration (delete tags older than X days).
- Restricted zones, permissions, and key bindings.

**9 Languages included**: English, French, Spanish, German, Italian, Portuguese (BR & PT), Russian, and Arabic.

---

## Purchase

### **[Buy on Tebex](https://vigilabs.tebex.io/package/vigi-spray)**

### **[Documentation](https://vigilabs.gitbook.io/vigilabs-docs)** | **[Discord Support](https://discord.gg/BntQVk5TqV)**

| | |
|--- | ---|
| Code is accessible | Partially (config, bridges, locales, gangs are open) |
| Subscription-based | No |
| Requirements | ESX, QBCore, Qbox, or ox_core |
| Support | Yes |
