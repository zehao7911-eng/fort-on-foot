# FORT ON FOOT

Build it. Walk it. Defend it. An original, portrait-friendly 3D moving-fortress game with an English interface. Six finite village-to-village routes; no account, payment, energy lives, external font, image generator or remote renderer dependency.

## Play

1. Tap either of the two physical supply crates at camp.
2. Tap a deck socket. An identical weapon upgrades up to three barrels; a different type replaces that socket. A duplicate on a three-star weapon overclocks it for this route (+20% damage per spare, up to two). Both supplies can always be used, even on a full deck.
3. Press MARCH. Guns fire automatically at visible nearby raiders. Tap a raider or ground point to focus all guns and request a volley (0.7-second cooldown).
4. Use STOMP when its charge is full to damage and knock back enemies within the shock ring. Charge returns with time and kills. Space also stomps.

The cannon is fast single-target fire, the mortar damages an area and the frost gun slows groups. Protect the hull until all waves are cleared and the destination is reached. Finishing earns one star, saving at least 50% hull adds a second, and saving at least 85% adds a third. Each route stores its best stars and score; reopening a receipt cannot repeatedly award progress. Failed attempts have free repairs. Weapons travel to the next camp and are retained when replaying earlier routes. Overclocks reset at camp. Six and twelve total stars unlock a cobalt canopy and a physical crew banner.

## World and assets

An original articulated brass-and-timber walking post office, planked deck, central engine house, lanterns, stair, four weapon mounts and a goggled human engineer. Two-link mechanical legs keep both segments connected to a shared knee; flat soles clear the floor during the gait. Upgraded guns have one, two or three actual barrels. Original masked runners, shield guards, heavy brutes and the final Iron Titan have separate walking feet, hit responses, health bars and frost rings.

Six authored roads include a windmill, an old aqueduct, a timber mill, a water crossing, a ruined crown wall and the Highgate towers. Three landscape palettes, shifting daytime/night atmosphere, planted walking steps, recoil, muzzle flashes, arcing mortar shells, frost splashes, debris, dust, target rings and a radial stomp effect. Wood grain and glow maps are generated in code. Geometry is batched by material. Lighting uses inexpensive directional/hemisphere lights, fog and soft contact sprites, without real-time shadow maps. Graphics LIGHT caps DPR at 1 and painting at about 30 Hz; FULL caps DPR at 1.5 and painting at 50 Hz. These caps are configuration, not physical-device FPS certification.

Reference: Combos **Minecraft: Walking Fortress**, by Kideo Hojima, <https://combos.game/zh-CN/play/1afd7d91ca5a2e4c04a9dbef0da1f202>. Actually inspected the fortress/village cinematic, walked the first-person deck, advanced to tutorial step 2, opened the map and started Night 1 toward Millford. The original's whole crafting system, battle completion and campaign were not played or reproduced. This independent game uses a simplified isometric build-and-defend loop, original code and models; it does not contain the reference's source, branding, characters, textures or music. Generic original mesh/audio/adapter patterns from our prior work are reused. Three.js r147 is vendored with its MIT notice.

## Run and build

`index.html` and `standalone.html` are identical self-contained entries with the renderer, application and CSS embedded. Extract the ZIP and open either entry, or put its root on any static HTML5 host. A WebGL-capable browser is required. No SDK or network request is required for the core game. The optional icon and cover are local files. `index-source.html` is the modular development entry and needs a static server.

Run `node build.cjs` after source changes. Run `node tests.mjs` and `node model-check.mjs` for game-specific simulation/SDK-mock and actual mesh checks. Model tests stub canvas text drawing; texture pixels are reviewed in the real browser.

Only `fort-on-foot-v1` is read from localStorage. Saves contain fitted weapons, build supplies, route, hull, charge, enemy and projectile state, cooldowns, focus, best results, settings and reward flags. Reloading during a march opens a safe pause menu. Resuming advances that exact encounter rather than silently restarting it. Build checkpoints keep both supply pick bits and installations. No other game's saves are enumerated, uploaded or cleared.

## GameWave SDK

Official document rechecked November 9, 2026, displaying October 30: <https://rg975ojk5z.feishu.cn/wiki/MQg7wMknzieOkukxyWVc4UB0nDh>.

Standalone startup never awaits `window.neonlib`. Each API is detected individually. The first actual supply collection, installation or departure starts a visit; after reload, the next real build action starts its resumed visit once. An already moving saved encounter starts its continuation when simulation actually advances. Selecting a part, looking at menus and opening a saved result do not fabricate lifecycle calls. Actual success, failure or abandoning an active route ends once. Preparing another route resets the visit guard.

Only recognized `{game:'fort-on-foot',v:1,profile}` cloud state is merged. Best results and reward flags are monotonic. Current local encounter state wins; an untouched first boot can explicitly recover a remote run. Unknown or failed cloud loads are not overwritten. Save requests, async registration failures, timeouts, partial/late injection and late listener cleanup are contained.

The optional host prompts appear only after supported async registration succeeds. Confirmed positive `onLike` unlocks cobalt; successful direct `onComment`, including empty text for an image-only comment, unlocks the banner. Both cosmetics also unlock through ordinary stars. Direct callback fields are used, project IDs remain strings and count snapshots are not identifiers. Unlike and malformed callbacks grant nothing. Persistent claim flags guard duplicate callbacks within this recognized browser/cloud save scope; this is not server-verified cross-device exactly-once accounting. Returned `data.unsubscribe()` functions are retained and invoked, including when registration resolves after disposal.

Validation evidence distinguishes static inspection, deterministic simulation, Node SDK mocks, native browser interactions, public served-file checks and actual platform tests. A supported GameWave App import, live account cloud and genuine App social callbacks have not been certified; browser mocks do not establish those results. Physical handset performance has not been measured.
