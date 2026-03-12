<p align="center">
  <img src="docs/assets/greenvalley-banner.png" alt="Green Valley Banner" width="800" />
</p>

<h1 align="center">Green Valley</h1>

<p align="center">
  <strong>A Pixel-Art Farming Simulation — Built From Scratch</strong>
</p>

<p align="center">
  A farming and life simulation game built entirely from scratch in JavaScript with no game engine. Custom rendering, custom physics, custom everything — just HTML5 Canvas and code. Features a deep genetic breeding system where you cross-breed plants, discover rare strains, and build a thriving farm with NPCs, quests, and a living world.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/engine-None%20(from%20scratch)-red" alt="No Engine" />
  <img src="https://img.shields.io/badge/rendering-HTML5%20Canvas%202D-blue" alt="Canvas" />
  <img src="https://img.shields.io/badge/language-JavaScript%20ES6%2B-yellow" alt="JavaScript" />
  <img src="https://img.shields.io/badge/genetics-Full%20Breeding%20System-green" alt="Genetics" />
  <img src="https://img.shields.io/badge/status-Playable-brightgreen" alt="Status" />
</p>

---

## Why From Scratch?

No Unity. No Godot. No Phaser. No engine at all.

Every system in Green Valley — rendering, input handling, collision detection, game loop, UI, audio, saving — was built by hand. This means understanding every line of code that makes the game work, and having total control over how it behaves.

The game runs entirely in a web browser using the HTML5 Canvas 2D API. No installations, no plugins, just open and play.

---

## Game Features

### 🌾 Farming

Full crop lifecycle from seed to harvest:

```
Seed → Seedling → Vegetative → Flowering → Harvestable
```

- **Soil management** — Nutrients deplete as crops grow; restore with fertilizer
- **Watering system** — Crops need water; track moisture levels per plot
- **Seasons** — Spring, Summer, Fall, Winter affect what grows and how fast
- **Weather effects** — Rain waters your crops; heatwaves stress them; snow halts growth
- **Quality system** — Plant health, water efficiency, and care affect harvest quality

### 🧬 Genetic Breeding System

The signature feature. Cross-breed plants to create offspring with inherited traits:

| Trait | What It Controls |
|-------|-----------------|
| Yield | How much you harvest |
| Quality | Grade of the harvest |
| Growth Speed | How fast it grows |
| Water Efficiency | How much water it needs |
| Disease Resistance | Survival against disease |
| Pest Resistance | Survival against pests |
| THC% | Specialized strain potency |
| CBD% | Specialized strain properties |

**How breeding works:**
- Select two parent plants
- Offspring inherits a mix of both parents' traits
- **5% mutation chance** on each trait (±0.2 variance)
- Color genetics — visual phenotype mixing from parents
- Multi-generation tracking — plants know their lineage

**Strain tiers:**
- **Starter strains** — Basic cultivars for new players
- **Rare strains** — Unlocked through skilled breeding and quests
- **Legendary strains** — Exceptional genetics, extremely rare

### 👥 NPCs & Relationships

8-22 NPCs with daily lives:

- **Schedules** — Each NPC has hourly routines (work, shop, walk, sleep) that vary by day
- **Relationships** — 0-300+ point system: Stranger → Friend → Best Friend → Close
- **Gift system** — Every NPC has loved, liked, neutral, disliked, and hated gifts
- **Occupations** — Herbalist, farmer, merchant, each with role-specific activities
- **Dialogue** — Relationship-level dialogue variants, quest conversations, casual chat

### 🏠 Buildings & Construction

| Building | Function |
|----------|---------|
| Greenhouse | Climate control, humidity regulation, automated watering, weather protection |
| Barn | Storage + animal care |
| Coop | Poultry management |
| Shed | Tool and item storage |
| Silo | Bulk crop storage |
| Well | Water source |
| House | Player home, rest, save point |

Buildings have **tiered upgrades**: Basic → Advanced → Specialized (e.g., Hydroponics greenhouse)

### 🔨 Crafting

100+ recipes across multiple stations:
- **Tools** — Hoe, Watering Can, Axe, Pickaxe, Scythe (with durability tiers)
- **Seeds** — Craft specialized seeds from harvested genetics
- **Products** — Transform raw harvests into sellable goods
- **Quality inheritance** — Output quality based on input ingredient quality

### 📋 Quests & Progression

| Type | Description |
|------|------------|
| **Main story** | 5+ chapter narrative arc |
| **Side quests** | NPC-driven tasks and favors |
| **Daily quests** | Repeatable daily objectives |
| **Weekly quests** | Longer-term challenges |

Multi-stage objectives (e.g., plant seeds → water → harvest → deliver) with XP, gold, item, and blueprint rewards.

### 🏆 Skills & Progression

| Skill | Levels | Effect |
|-------|--------|--------|
| **Farming** | 1-10+ | Crop growth speed, yield, plot management |
| **Breeding** | 1-10+ | Mutation rates, strain discovery, genetics mastery |
| **Processing** | 1-10+ | Harvest yield, drying/trimming efficiency |
| **Social** | 1-10+ | NPC relationship bonuses, gift effectiveness |

### 💰 Economy

- **Multiple shops** with dynamic pricing and buy/sell restrictions
- **Gold currency** with wallet management
- **Market fluctuations** based on season and supply
- **Stock tracking** — shops restock periodically

### 🌤️ Time & Weather

- **Day/night cycle** — 10 minutes of real time per in-game day
- **4 seasons** — 30-day cycles each, affecting crops and NPC behavior
- **Dynamic weather** — Season-specific patterns:
  - Winter: Snow (30%), Clear (70%)
  - Spring: Rain (50%), Storm (20%), Clear (30%)
  - Summer: Heatwave (20%), Rain (20%), Clear (60%)
  - Fall: Wind (30%), Rain (30%), Clear (40%)

### ⚡ Energy System

- **100-point stamina pool** — Actions drain energy (tools, sprinting, farming)
- **Regeneration** — Sleep, food consumption
- **Fatigue** — Reduced efficiency when tired

---

## Architecture

Built as a **modular vanilla JavaScript application** with an event-driven architecture:

```
main.js (entry point)
│
├── Game.js (core game loop + state)
│
├── Core Systems
│   ├── InputManager      — Keyboard + mouse handling
│   ├── AudioManager      — Web Audio API sounds
│   ├── SaveManager       — LocalStorage persistence
│   ├── EventBus          — Pub/sub event system
│   └── GameBootstrap     — Initialization sequence
│
├── Rendering
│   ├── EnhancedRenderer  — Canvas 2D rendering + camera
│   ├── Animation         — Sprite frame animation
│   ├── SpriteSheet       — Texture atlas system
│   ├── Particles         — Particle effects
│   ├── Lighting          — Day/night visual effects
│   └── Transitions       — Scene fade/wipe transitions
│
├── World
│   ├── GameWorld         — Zone management
│   ├── TileMap           — Tile-based collision + interaction
│   ├── Camera            — Viewport tracking
│   └── Zones: Farm, Forest, Cave, Town, Greenhouse
│
├── Game Systems
│   ├── FarmingSystem     — Crop lifecycle management
│   ├── QuestSystem       — Quest tracking + completion
│   ├── AchievementSystem — Achievement tracking
│   ├── TimeSystem        — Day/night, seasons, year
│   ├── WeatherSystem     — Dynamic weather patterns
│   ├── EconomySystem     — Pricing + transactions
│   ├── EnergySystem      — Stamina management
│   ├── ShopSystem        — Buy/sell interface
│   ├── CraftingSystem    — Recipe processing
│   └── ToolSystem        — Tool durability + tiers
│
├── Entities
│   ├── Player            — Stats, skills, inventory
│   ├── NPCs              — Dialogue, relationships, schedules
│   └── Plants            — Growth, genetics, health
│
├── Genetics Module
│   ├── Genome            — Trait container
│   ├── Breeding          — Cross-breed logic
│   ├── Mutations         — Random trait variance
│   ├── ColorGenetics     — Visual phenotype mixing
│   └── StrainRegistry    — Starter/Rare/Legendary
│
└── UI
    ├── HUD               — Heads-up display
    ├── MenuSystem        — Main/pause/settings
    ├── DialogSystem      — NPC conversations
    ├── InventoryUI       — 32-slot grid (8×4)
    ├── JournalUI         — Quest + achievement log
    └── MapUI             — Zone overview
```

> Full architecture deep-dive in [ARCHITECTURE.md](ARCHITECTURE.md)

---

## Tech Stack

| Component | Technology | Notes |
|-----------|-----------|-------|
| **Language** | JavaScript ES6+ | Vanilla — no frameworks |
| **Rendering** | HTML5 Canvas 2D API | Pixel-perfect with `imageSmoothingEnabled: false` |
| **Audio** | Web Audio API | Deferred init (browser requirement) |
| **Persistence** | LocalStorage | Compressed save data (Base64) |
| **Architecture** | ES6 Modules | Native browser imports, no build pipeline |
| **Input** | Keyboard + Mouse events | Centralized InputManager |
| **PWA** | Service Worker + Manifest | Installable, offline-capable |
| **Assets** | PNG spritesheets | Optimized texture atlases |

**No game engine. No bundler. No transpiler.** Just JavaScript, Canvas, and hand-crafted game systems.

> Full breakdown in [TECH_STACK.md](TECH_STACK.md)

---

## Controls

| Key | Action |
|-----|--------|
| WASD / Arrow Keys | Move |
| E / Space | Interact |
| I | Inventory |
| 1-9 | Tool/item hotbar |
| Left Click | Use tool / interact |
| Right Click | Context action |

---

## Screenshots

<p align="center">
  <em>Screenshots coming soon.</em>
</p>

<!--
<p align="center">
  <img src="docs/screenshots/farm.png" alt="Farm" width="600" />
  <br><em>Your farm in summer — crops growing, greenhouse in the background</em>
</p>

<p align="center">
  <img src="docs/screenshots/breeding.png" alt="Breeding" width="600" />
  <br><em>Genetic breeding interface — crossing two parent plants</em>
</p>

<p align="center">
  <img src="docs/screenshots/town.png" alt="Town" width="600" />
  <br><em>Town center with NPCs going about their daily routines</em>
</p>
-->

---

## Project Status

Green Valley is **playable** with major systems functional:

- ✅ Custom game engine (rendering, input, physics, audio)
- ✅ Full farming lifecycle (seed → harvest)
- ✅ Genetic breeding system with mutations and strain tiers
- ✅ NPC system with schedules, relationships, and dialogue
- ✅ Building construction with tiered upgrades
- ✅ 100+ crafting recipes
- ✅ Quest system with multi-stage objectives
- ✅ Day/night cycle, seasons, and weather
- ✅ Economy with shops and dynamic pricing
- ✅ Achievement system
- ✅ Save/load with compressed LocalStorage
- ✅ PWA support (installable, offline-capable)
- 🔄 Story chapters and endgame content

---

## License

This repository contains documentation and architecture references only. The source code is proprietary and not publicly available.

**© 2024-2026 DevStudio AI. All rights reserved.**

See [LICENSE](LICENSE) for details.
