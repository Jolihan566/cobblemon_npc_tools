# ⚡ Cobblemon Spawn Generator

A visual, browser-based datapack editor for [Cobblemon](https://cobblemon.com/) — configure Pokémon spawns, drop overrides, herd spawns, and full custom Pokémon species without writing a single line of JSON.

---

## Features

| Feature | Description |
|---|---|
| **Spawn Editor** | Configure where and how each Pokémon spawns — biomes, time of day, weather, light level, and more |
| **Herd Spawns** | Create group spawns where a leader and filler members appear together |
| **Drop Overrides** | Override default Cobblemon drops per Pokémon, including empty drops to suppress all loot |
| **Custom Pokémon** | Define entirely new Pokémon species (fakemon) with full species files |
| **Bulk Apply** | Apply spawn settings to many Pokémon at once |
| **Pool Weight Viewer** | Visualise spawn probability within each bucket/context pool, including herd member effective weights |
| **Biome Browser** | Browse all Cobblemon biomes and see your spawn coverage via a heatmap |
| **Type Filters** | Filter the Pokémon list by type with ANY (inclusive) or ALL (exclusive) mode |
| **Import / Export** | Load an existing datapack `.zip` and export a ready-to-drop datapack |
| **Pack Settings** | Configure namespace, description, mod compatibility, and base spawn negation |
| **Stats Dashboard** | Pack-wide statistics — total configured, per-generation, per-bucket breakdown |

---

## Getting Started

### Requirements

- A modern web browser (Chrome, Firefox, Edge, Safari)
- No installation required — open `cobblemon_spawn_generator.html` directly in your browser

### Basic Workflow

1. **Open the file** — Double-click `cobblemon_spawn_generator.html` or drag it into your browser
2. **Name your pack** — Type a name in the top-left input (e.g. `my-region-spawns`)
3. **Find a Pokémon** — Use the sidebar search, generation filters, or type filters
4. **Add a spawn entry** — Click **+ Spawn Entry** in the editor header
5. **Configure conditions** — Set biomes, time of day, light level, and other conditions
6. **Export** — Click **📦 Export Datapack** to download a `.zip` file
7. **Install** — Drop the zip into your world's `datapacks/` folder and reload the world

> ⚠️ **Important:** Cobblemon datapacks require a **world reload from the main menu** — the `/reload` command does not work with Cobblemon datapacks.

---

## Interface Overview

```
┌─────────────────────────────────── Topbar ────────────────────────────────────┐
│ ⚡ Cobblemon Spawn Generator   [Pack Name]   Bulk Apply  Custom Pokémon  ...   │
├──────────────┬──────────────────────────────────┬──────────────────────────────┤
│              │                                  │                              │
│   Sidebar    │         Spawn Editor             │       Preview Panel          │
│              │                                  │                              │
│ Search       │  #001 Bulbasaur  ✓ Cobblemon     │  Spawn / Species / Edit JSON │
│ Filters      │  ─────────────────────────────   │                              │
│ Type Grid    │  Entry 1: common · grounded      │  { "enabled": true,          │
│ Pokémon List │  ▼ Conditions                    │    "spawns": [ ... ] }       │
│              │    Biomes: #cobblemon:is_forest  │                              │
│              │    Time: day                     │                              │
│              │  🎁 Species Drops                │                              │
└──────────────┴──────────────────────────────────┴──────────────────────────────┘
```

### Sidebar

- **Search bar** — Filter by name, Pokédex number, or type
- **Status filters** — All / Has Spawn / No Spawn / Cobblemon / Mega / Not Impl. / ✦ Custom
- **Generation filters** — G1–G9
- **Type filters** — All 18 types with ANY (OR) or ALL (AND) mode
- **Implementation dots** — 🟢 Green = in base Cobblemon, 🟣 Purple = Mega Showdown, 🔴 Red = not implemented
- **Ctrl+click** — Multi-select Pokémon for bulk operations

### Editor

- **Spawn File toggle** — Enable/disable the entire spawn file for a Pokémon (sets `"enabled": false` at the top of the JSON)
- **+ Spawn Entry** — Add a new spawn entry
- **🐾 Add Herd** — Add a herd spawn entry
- **⬆ Evo Line** — Scale spawn data across an entire evolution line
- **⎘ Copy From** — Clone spawn entries from another Pokémon
- **🎁 Species Drops** — Override drops with full control over items, quantities, and percentages

### Preview Panel

- **Spawn tab** — Live JSON preview of the spawn file
- **Species tab** — Live JSON preview of the species additions (or full species file for custom Pokémon)
- **Edit JSON tab** — Directly edit the raw JSON

---

## Spawn Entries

Each spawn entry defines one way a Pokémon can appear in the world.

### Core Fields

| Field | Description |
|---|---|
| **Bucket** | Rarity tier: `common`, `uncommon`, `rare`, `ultra-rare` |
| **Context** | Spawn location: `grounded`, `submerged`, `surface`, `fishing` |
| **Weight** | Relative spawn probability within its bucket |
| **Level Range** | Min and max spawn level, e.g. `5-40` |
| **Presets** | Comma-separated Cobblemon preset names (see [Presets](#presets)) |

### Condition Fields

| Field | Description |
|---|---|
| **Biomes** | One biome ID or tag per line, e.g. `#cobblemon:is_forest` |
| **Time Range** | `day`, `night`, `dawn`, `dusk`, or numeric `0-6000` |
| **Min/Max Sky Light** | 0–15. Sky light is 15 outdoors in daylight, 0 underground |
| **Min/Max Light** | 0–15. Total light level (sky + block light) |
| **Can See Sky** | Spawn point must have unobstructed view of the sky |
| **Is Raining / Thundering** | Weather conditions |
| **Needed Nearby Blocks** | One block ID per line — at least one must be in range |
| **Needed Base Blocks** | The block directly beneath the spawn point |
| **Moon Phase** | 0–7 (0 = full moon) |

### Anti-Conditions

Anti-conditions prevent spawning where the conditions are true — useful for excluding specific biomes or weather.

---

## Biomes and Tags

Cobblemon uses Minecraft's biome tag system. Tags are prefixed with `#` and match any biome in that group.

**Common tags:**

| Tag | Matches |
|---|---|
| `#cobblemon:is_overworld` | All overworld biomes |
| `#cobblemon:is_forest` | Forest-type biomes |
| `#cobblemon:is_ocean` | All ocean biomes |
| `#cobblemon:is_river` | River biomes |
| `#cobblemon:is_mountain` | Mountain biomes |
| `#cobblemon:is_cave` | Cave/underground biomes |
| `#cobblemon:is_desert` | Desert biomes |
| `#cobblemon:is_jungle` | Jungle biomes |
| `#cobblemon:is_snowy` | All snowy biomes |
| `#cobblemon:is_nether` | All Nether biomes |
| `#cobblemon:is_end` | End biomes |

Use the **Tag Picker** button inside any spawn entry to browse available tags, or use the **🌍 Biome Browser** to explore all biomes and their current spawn coverage.

---

## Buckets and Weights

Cobblemon's spawn system is bucket-based — each spawn attempt selects a bucket first, then picks a Pokémon from within that bucket. Pokémon in different buckets never compete directly.

| Bucket | Typical Usage | Suggested Weight |
|---|---|---|
| `common` | Frequent encounters, starter areas | 5–15 |
| `uncommon` | Less frequent but expected encounters | 3–8 |
| `rare` | Uncommon finds, version-specific Pokémon | 1–5 |
| `ultra-rare` | Legendaries, very rare spawns | 0.1–2 |

**Weight** = `(this entry's weight) ÷ (sum of all weights in the same bucket)` = spawn probability when that bucket is selected.

---

## Presets

Presets apply additional spawn rules to an entry. Reference them by name in the Presets field (comma-separated).

| Preset | Description |
|---|---|
| `natural` | Spawns on natural terrain — grass, dirt, stone |
| `wild` | General wild spawn — no block requirement |
| `water` | Water-dwelling — applies water-surface tags |
| `fishing` | Can be caught via fishing rod |
| `cave` | Cave-dwelling — applies underground conditions |
| `legendary` | Legendary settings — very low weight, open-world conditions |

See [Cobblemon's Spawn Detail Presets wiki page](https://wiki.cobblemon.com/index.php/Spawn_Detail_Presets) for the full list.

---

## Herd Spawns

Herd spawns create a group of Pokémon instead of a single one. A leader spawns first, then filler members fill up the herd.

### Setup

1. Click **🐾 Add Herd** in the editor header
2. Set **Spawn Position**, **Bucket**, and **Weight**
3. Set **Max Herd Size** — maximum total Pokémon in the group
4. Set **Min Distance Between Spawns** — how spread out members are
5. Add **Herd Members** — each with a Pokémon ID, weight, max times, and level offset

### Member Fields

| Field | Description |
|---|---|
| **Pokémon ID** | Internal Cobblemon ID (lowercase, no spaces), e.g. `rattata` |
| **Weight** | Relative chance this member fills a slot within the herd |
| **Max Times** | How many of this member can appear. Leave blank for unlimited |
| **Is Leader** | Marks this member as the herd leader — spawns first |
| **Level Offset** | Shifts this member's level relative to the herd's base range |

### Pool Weight Calculator

The **⚖ Pool Weights** viewer correctly accounts for herd members. Each member's effective pool weight is calculated as:

```
effective weight = herd entry weight × (member weight ÷ total member weights)
```

Rows derived from herds are marked with an orange **HERD** badge. Hover the weight value to see the full calculation breakdown.

---

## Drop Overrides

Override a Pokémon's default Cobblemon drops using the **🎁 Species Drops** section in the editor.

Cobblemon's drop system works differently from vanilla Minecraft:
1. Cobblemon attempts to collect **amount** successful drops from the entries list
2. For each entry, it rolls a percentage check
3. Once **amount** entries pass, or all entries are exhausted, rolling stops
4. All passing entries drop their items

### Drop Entry Fields

| Field | Description |
|---|---|
| **Item ID** | e.g. `minecraft:bone` or `cobblemon:poke_ball` |
| **Min / Max Qty** | Random quantity range |
| **% Chance** | Probability this entry passes (100 = always) |

### Empty Drops

Toggle **Empty drops** to export `amount: 0, entries: []` — this completely suppresses all default Cobblemon drops for that Pokémon.

### Bulk Operations

Use the **⚡ Presets** menu for quick templates or bulk operations:
- **Set Empty Drops (all visible)** — apply empty drops to every Pokémon currently visible in the sidebar
- **Clear All Drop Overrides (all visible)** — remove all overrides and revert to Cobblemon defaults

---

## Custom Pokémon

Create entirely new Pokémon species for fakemon or custom regions. Custom Pokémon export as **full `species/` files**, not species additions.

### Creating a Custom Pokémon

1. Click **✦ Custom Pokémon** in the topbar
2. Enter a **Display Name** — the internal ID auto-generates
3. Set **Primary Type** (required) and optional **Secondary Type**
4. Fill in the **Stats**, **Moves**, **Evolutions**, and **Misc** tabs
5. Click **✦ Save Pokémon** — it appears in the sidebar under a purple separator
6. Select it to add spawn entries like any other Pokémon

### Tabs

| Tab | Contents |
|---|---|
| **Identity** | Name, ID, types, catch rate, gender ratio, exp group, egg groups, abilities, Pokédex entry |
| **Stats** | Base stats with live BST bar chart, EV yields, size (height, weight, scale, hitbox) |
| **Moves** | Level-up, egg, TM, and tutor moves in `method:movename` format |
| **Evolutions** | Evolution methods with variant, result Pokémon, required context/item, and level |
| **Misc** | Lighting data, shoulder mountable flag, cannot dynamax, and custom drops |

### Move Format

```
5:quickattack       ← Level-up: learned at level 5
egg:thunder         ← Egg move: inherited on hatch
tm:thunderbolt      ← TM move
tutor:icebeam       ← Tutor move
```

All move names must be **lowercase with no spaces**, e.g. `quickattack`, `10000000voltthunderbolt`.

> ⚠️ Custom Pokémon need a matching **model and texture** to render in-game. This tool generates data files only. Use the [Cobblemon Fakemon Generator](https://tools.cobblemon.com/fakemon/) or Blockbench with the Cobblemon plugin for models.

---

## Bulk Apply

Apply spawn settings to many Pokémon at once.

- **Targets:** Ctrl+click to batch-select specific Pokémon, or leave none selected to target all currently visible Pokémon
- **Normal spawn tab** — bulk-add a standard spawn entry
- **Herd spawn tab** — bulk-add a herd entry (each target Pokémon is auto-added as leader and member)
- Check **Replace existing** to overwrite instead of append

### Quick-Action Bar

| Button | Action |
|---|---|
| ◎ Legendaries / Mythicals / Ultra Beasts | Toggle preset ultra-rare spawns on/off for each category |
| ⬆ Set Rarity | Force all spawn entries for a category to ultra-rare bucket |
| 🗑 Clear All | Remove ALL spawn data from every Pokémon |

---

## Pack Settings

Accessible via **⚙ Pack Settings** in the topbar.

| Setting | Description |
|---|---|
| **Pack Name** | Used as the exported zip filename |
| **Description** | Shown in Minecraft's datapack list (`pack.mcmeta`) |
| **Namespace** | Folder under `data/`. Default is `cobblemon` — only change if you know what you're doing |
| **Negate Base Spawns** | Adds a `filter` block to `pack.mcmeta` that blocks all default Cobblemon spawn files |
| **Needed Installed Mods** | Spawns only apply if these mod IDs are installed (e.g. `biomesoplenty`) |
| **Needed Uninstalled Mods** | Spawns only apply if these mods are NOT installed (useful for fallback spawns) |

> ⚠️ Enabling **Negate Base Spawns** means any Pokémon without a configured spawn entry will not appear in the world at all.

---

## Export Format

The exported `.zip` has the following structure:

```
my-pack.zip
├── pack.mcmeta
└── data/
    └── cobblemon/
        ├── spawn_pool_world/
        │   ├── bulbasaur.json       ← one file per Pokémon with spawns
        │   ├── charmander.json
        │   └── ...
        ├── species_additions/
        │   └── vulpix.json          ← drop overrides for existing Pokémon
        └── species/
            └── emberwhelp.json      ← full species files for custom Pokémon
```

### Spawn Pool World File

```json
{
  "enabled": true,
  "spawns": [
    {
      "id": "bulbasaur-1",
      "pokemon": "bulbasaur",
      "type": "pokemon",
      "bucket": "common",
      "context": "grounded",
      "weight": 10.0,
      "level": "5-25",
      "presets": ["natural"],
      "condition": {
        "biomes": ["#cobblemon:is_forest"],
        "timeRange": "day",
        "canSeeSky": true
      }
    }
  ]
}
```

### Species Additions File (Drop Overrides)

```json
{
  "pokemon": "vulpix",
  "drops": {
    "amount": "1",
    "entries": [
      { "item": "minecraft:sweet_berries", "quantityRange": "2-3" },
      { "item": "cobblemon:fire_stone_shard", "quantityRange": "1", "percentage": 15 }
    ]
  }
}
```

---

## Importing

Click **📂 Import** and select an existing datapack `.zip`. The tool reads all spawn files and species additions and loads them into the editor so you can continue editing and re-export.

---

## Useful Links

- [Spawn Pool World — Cobblemon Wiki](https://wiki.cobblemon.com/index.php/Spawn_Pool_World)
- [Spawn Conditions — Cobblemon Wiki](https://wiki.cobblemon.com/index.php/Spawn_Condition)
- [Spawn Detail Presets — Cobblemon Wiki](https://wiki.cobblemon.com/index.php/Spawn_Detail_Presets)
- [Species Files — Cobblemon Wiki](https://wiki.cobblemon.com/index.php/Species)
- [Species Additions — Cobblemon Wiki](https://wiki.cobblemon.com/index.php/Species_Additions)
- [Cobblemon GitLab (source + default species files)](https://gitlab.com/cable-mc/cobblemon/-/tree/main/common/src/main/resources/data/cobblemon/species)
- [Cobblemon Fakemon Generator](https://tools.cobblemon.com/fakemon/)

---

## Tips and Tricks

- **Ctrl+click** multiple Pokémon in the sidebar to batch-select them, then use **Bulk Apply** to configure them all at once
- **⬆ Evo Line** automatically scales spawn weights across an evolution chain — base forms spawn more often, final forms less
- **⎘ Copy From** clones all spawn entries from another Pokémon — great for evolution lines that share the same habitat
- The **⚖ Pool Weights** viewer updates live as you add or change entries — use it to check that your rarities actually feel right
- The **Biome Coverage Heatmap** quickly shows which biomes have no spawns configured — look for red tiles
- Use **ANY type filter + Has Spawn filter** together to find all configured Water-types, for example
- The **Species tab** in the preview panel shows exactly what will be exported for drops and custom species
- Custom Pokémon appear below standard Pokémon in the sidebar under a purple **✦ Custom Pokémon** separator — click the ✎ pencil to edit their species data at any time

---

*Built for the Cobblemon modding community. Not affiliated with the official Cobblemon project.*
