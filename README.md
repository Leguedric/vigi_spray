<h1><strong>Vigi Spray - Ultimate Urban Art System</strong></h1>
<p><strong><span style="color:rgb(147,101,184);font-size:16px;">The most advanced, high-performance graffiti system available for FiveM. Freehand paint, stencils, masking tape, mirror mode, live sync, and a full admin panel.</span></strong></p>
<p><strong><span style="color:rgb(250,197,28);">NEW in v1.9.0 :</span></strong> full <strong>ox_core</strong> support, alongside ESX, QBCore and Qbox. Auto-detected, with no extra dependency and nothing to add to your fxmanifest.</p>
<h1><span style="color:rgb(250,197,28);"><a href="https://www.youtube.com/watch?v=bpM9EK1qdN4" target="_blank" rel="noreferrer noopener"><strong>SHOWCASE VIDEO</strong></a></span> | <span style="color:rgb(147,101,184);"><a href="https://vigilabs.gitbook.io/vigilabs-docs" target="_blank" rel="noreferrer noopener"><strong>DOCUMENTATION</strong></a></span></h1>
<hr />
<h2><strong>CREATIVE TOOLS</strong></h2>
<h3><strong>Spray Painting</strong></h3>
<ul>
  <li><strong>Freehand Drawing</strong>: Paint on any flat surface with full mouse control</li>
  <li><strong>Live Multiplayer Sync</strong>: Watch other players create art in real-time</li>
  <li><strong>Color System</strong>: Full spectrum picker with presets, hex input, recent colors, and favorites</li>
  <li><strong>Pressure Mechanics</strong>: Shake the can to build pressure, sputtering effect when running low</li>
  <li><strong>Adjustable Cap Size</strong>: Scroll to change stroke width from thin to fat cap</li>
  <li><strong>Depth Adjustment</strong>: Scroll to offset the graffiti from the wall, fixing Z-fighting on uneven surfaces</li></ul>
<h3><strong>Precision Tools</strong></h3>
<ul>
  <li><strong>Masking Tape</strong>: Create clean straight lines with angle snapping (45-degree increments)</li>
  <li><strong>Mirror Mode</strong>: Place a symmetry axis and every stroke is reflected in real-time</li>
  <li><strong>Rule of Thirds Grid</strong>: Toggle an overlay grid for composition and scaling</li>
  <li><strong>3D Dimensions Display</strong>: See the exact size of your work area while placing it</li></ul>
<h3><strong>Edit Mode</strong></h3>
<ul>
  <li><strong>Re-Edit Your Work</strong>: Aim at your own graffiti and re-enter the canvas to continue drawing</li>
  <li><strong>Non-Destructive</strong>: Your existing artwork is loaded back onto the canvas</li>
  <li><strong>Ownership Check</strong>: Only the original creator can edit (admins can lock tags to prevent editing)</li></ul>
<h3><strong>Stencils &amp; Sketchbook</strong></h3>
<ul>
  <li><strong>Stencil Gallery</strong>: Browse and place admin-managed designs with a progressive spray reveal animation</li>
  <li><strong>URL Import</strong>: (Optional) Players paste an image URL to place it directly, with domain whitelist/blacklist and cooldowns</li>
  <li><strong>Player Access Control</strong>: Restrict specific stencils to specific players</li>
  <li><strong>Local Sketchbook</strong>: Players save drawings locally and reuse them across sessions</li></ul>
<h3><strong>Cleaning</strong></h3>
<ul>
  <li><strong>Sponge System</strong>: Progressive erasure with a physical sponge animation</li>
  <li><strong>Durability &amp; Wear Widget</strong>: Sponges degrade over time with a real-time visual indicator (cyan &gt; orange &gt; red)</li>
  <li><strong>Locked Tags</strong>: Admins can lock graffiti to prevent cleaning</li></ul>
<hr />
<h2><strong>PERFORMANCE</strong></h2>
<ul>
  <li><strong>Atlas Rendering</strong>: All visible tags share a single GPU texture atlas for minimal draw calls</li>
  <li><strong>Camera-Side Face Culling</strong>: Only the face visible to the player is rendered (2 draw calls instead of 4 per tag)</li>
  <li><strong>Debounced File I/O</strong>: Rapid operations are batched to reduce disk writes</li>
  <li><strong>Latent Event Streaming</strong>: Large images synced via chunked events, no network bottleneck</li>
  <li><strong>WebP Compression</strong>: All artwork stored in WebP for optimal quality-to-size ratio</li>
  <li><strong>Data Integrity Check</strong>: Automatic cleanup of orphaned files on server start</li>
  <li><strong>Zero Dependencies</strong>: Completely standalone, no xSound or external libraries</li>
  <li><strong>3D Spatial Audio</strong>: Distance-based sound built entirely within NUI</li></ul>
<hr />
<h2><strong>ADMIN PANEL</strong></h2>
<h3><strong>Management</strong></h3>
<ul>
  <li><strong>Dashboard</strong>: Total graffiti, active artists, daily creation stats</li>
  <li><strong>Interactive World Map</strong>: Leaflet.js map with clustering, switchable Atlas/Satellite/Roads views</li>
  <li><strong>Search &amp; Filter</strong>: Find tags by artist, date, ID, or distance from your position</li>
  <li><strong>Bulk Delete</strong>: Select multiple tags and delete them in a single batch</li>
  <li><strong>Click-to-Delete</strong>: Aim and click to remove tags directly in the game world</li>
  <li><strong>Admin Depth Adjustment</strong>: Select any tag and scroll to fine-tune its wall offset</li>
  <li><strong>Tag Locking</strong>: Lock tags to prevent player editing and cleaning</li>
  <li><strong>Stencil Library</strong>: Add, rename, import, delete stencils, and manage per-player access</li>
  <li><strong>Discord Webhooks</strong>: Every creation logged with artist info, coordinates, and image preview</li></ul>
<h3><strong>Permissions &amp; Security</strong></h3>
<ul>
  <li><strong>ACE Permissions</strong>: Restrict spraying to specific FiveM groups</li>
  <li><strong>Job &amp; Boss Grade</strong>: Allow only specific jobs or boss ranks (ESX grades, QB isboss, ox_core groups and permissions)</li>
  <li><strong>Discord Role Check</strong>: Restrict to specific Discord roles</li>
  <li><strong>External Export</strong>: Hook into any custom permission resource</li>
  <li><strong>Restricted Zones</strong>: Define polygon areas where graffiti is forbidden</li>
  <li><strong>Blacklist System</strong>: Ban/unban players via Discord ID, License, or Server ID</li></ul>
<hr />
<h2><strong>COMPATIBILITY</strong></h2>
<h3><strong>Frameworks</strong></h3>
<ul>
  <li><strong>ESX</strong>: Legacy &amp; Extended, all versions</li>
  <li><strong>QBCore</strong>: Full support</li>
  <li><strong>Qbox</strong>: Compatible</li>
  <li><strong>ox_core</strong>: Full support, no extra dependency and nothing to add to your fxmanifest</li>
  <li><strong>Auto-Detection</strong>: Framework and inventory detected automatically</li>
  <li><strong>Custom Framework</strong>: Open bridge files for any implementation</li></ul>
<h3><strong>Inventory Systems</strong></h3>
<ul>
  <li><strong>ox_inventory</strong> | <strong>qs-inventory</strong> | <strong>qb-inventory</strong> | <strong>codem-inventory</strong> | <strong>chezza-inventory</strong> | <strong>ESX default</strong></li>
  <li><strong>Command Mode</strong>: Works without any inventory (<code>/spray</code>, <code>/sponge</code>)</li>
  <li><strong>ox_core</strong>: has no inventory of its own, pair it with ox_inventory or use Command Mode</li></ul>
<h3><strong>Integrations</strong></h3>
<ul>
  <li><strong>OP Gangs (op-crime)</strong>: Native territory integration, loyalty rewards, rival penalties</li>
  <li><strong>Custom Scripts</strong>: Server events and exports for police alerts, gang systems, economy, etc.</li></ul>
<h3><strong>Languages</strong></h3>
<ul>
  <li><strong>9 Languages</strong>: English, French, Spanish, German, Italian, Portuguese (PT &amp; BR), Russian, Arabic</li></ul>
<hr />
<h2><strong>API</strong></h2>
<p>Fifteen exports and two events, for wiring graffiti into police dispatch, a gang system, an economy script or your own tooling.</p>
<div style="background:#0f1720;padding:16px;border-radius:4px;overflow-x:auto;max-width:100%;"><pre style="margin:0;font-family:Consolas,Monaco,monospace;font-size:13px;line-height:1.65;color:#e6edf3;white-space:pre-wrap;word-break:break-word;"><code><span style="color:#6a9955;">-- Server</span>
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">GetTagCount</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">GetTagInfo</span>(tagId)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">GetNearbyTags</span>(coords, radius)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">IsStencilTag</span>(tagId)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">GetAllStencils</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">DeleteTag</span>(tagId)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">DeleteClosestTag</span>(coords, radius)

<span style="color:#6a9955;">-- Client</span>
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">IsSprayMode</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">GetNearbyTags</span>(radius)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">OpenStencilGallery</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">OpenAdminPanel</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">SetGraffitiHidden</span>(hidden)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">IsGraffitiHidden</span>()
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">StartCustomCleaning</span>(options)
exports[<span style="color:#ce9178;">'vigi_spray'</span>]:<span style="color:#4fc1ff;">StopCleaning</span>()

<span style="color:#6a9955;">-- Events</span>
<span style="color:#4fc1ff;">vigi_spray:server:onTagCreated</span>
<span style="color:#4fc1ff;">vigi_spray:server:onTagCleaned</span></code></pre></div>
<p>Both events carry the source, the tag id, the tag data and the OP Gangs territory when there is one.</p>
<p>Full signatures and payloads are in the <a href="https://vigilabs.gitbook.io/vigilabs-docs" target="_blank" rel="noreferrer noopener">documentation</a>. Everything else lives in one <code>config.lua</code>, outside the escrow along with both bridge files, the server config, the locales and the gang integration.</p>
<hr />
<p><span style="color:rgb(85,57,130);"><strong><a href="https://vigilabs.gitbook.io/vigilabs-docs" target="_blank" rel="noreferrer noopener">Full Documentation</a></strong></span> | <span style="color:rgb(85,57,130);"><strong><a href="https://discord.gg/BntQVk5TqV" target="_blank" rel="noreferrer noopener">Discord Support</a></strong></span></p>
