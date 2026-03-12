# Green Valley — Tech Stack

> Every technology choice — and why "nothing" is sometimes the most impressive choice

---

## Core Philosophy

**No engine. No framework. No bundler.** Every system is hand-built, giving complete control over behavior, performance, and learning.

---

## Language & Platform

| Component | Choice | Why |
|-----------|--------|-----|
| **Language** | JavaScript ES6+ | Universal browser support, no compilation needed |
| **Module System** | ES6 import/export | Native browser modules — no webpack, no rollup |
| **Platform** | Web Browser | Zero installation, cross-platform by default |
| **HTML** | HTML5 | Canvas hosting, minimal DOM |
| **CSS** | Custom | Pixel-art UI styling |

---

## Rendering

| Component | Choice | Why |
|-----------|--------|-----|
| **API** | HTML5 Canvas 2D | Full pixel-level control, lightweight, widely supported |
| **Anti-aliasing** | Disabled (`imageSmoothingEnabled: false`) | Crisp pixel art at any scale |
| **Sprite System** | Custom SpriteSheet class | Grid-based cell extraction from atlas textures |
| **Animation** | Custom frame cycling | Frame-by-frame sprite animation with delta time |
| **Camera** | Custom viewport tracking | Smooth following with zone-based boundaries |
| **Particles** | Custom particle system | Harvest effects, weather visuals |
| **Lighting** | Custom tint system | Day/night cycle visual shifts |
| **Transitions** | Custom fade/wipe | Scene changes between zones |

**Not used:** WebGL, Three.js, PixiJS, Phaser, or any rendering library.

---

## Game Architecture

| Component | Choice | Why |
|-----------|--------|-----|
| **Game Loop** | `requestAnimationFrame` | Browser-native, V-synced, battery-friendly |
| **Timing** | Delta time | Frame-rate independent gameplay |
| **Event System** | Custom EventBus (pub/sub) | Loose coupling between 10+ game systems |
| **Entity Model** | Rich objects | Player, NPC, Plant each with domain-specific data |
| **Manager Pattern** | Singleton managers | Central coordination for complex systems |
| **Data Format** | JSON configs | Quest, NPC, item, building definitions |

---

## Input

| Component | Choice | Why |
|-----------|--------|-----|
| **System** | Custom InputManager | Centralized key binding and event handling |
| **Keyboard** | `keydown`/`keyup` events | Movement (WASD/Arrows), interaction (E/Space), menus |
| **Mouse** | `click`/`contextmenu` events | Tool use, context actions |
| **Hotbar** | Number keys (1-9) | Quick tool/item selection |
| **Debouncing** | Custom | Prevents double-firing on rapid input |

---

## Audio

| Component | Choice | Why |
|-----------|--------|-----|
| **API** | Web Audio API | Low-latency, programmable audio |
| **Initialization** | Deferred (first user interaction) | Required by browser autoplay policies |
| **Buffer Management** | Custom AudioManager | Fetch, decode, cache audio files |
| **Fallback** | Graceful degradation | Game continues if audio assets missing |

---

## Persistence

| Component | Choice | Why |
|-----------|--------|-----|
| **Storage** | localStorage | Built-in browser storage, no server needed |
| **Format** | JSON → Base64 | Compressed save data |
| **Fallback** | Graceful degradation | Game playable without save capability |
| **Scope** | Full game state snapshot | Player, farm, NPCs, quests, time, world |

---

## Asset Pipeline

| Asset Type | Format | Specifications |
|-----------|--------|---------------|
| **NPC Portraits** | PNG spritesheet | 320×240, 80×80 cells |
| **NPC Sprites** | PNG spritesheet | 288×144, 32×48 cells (4 directions) |
| **Player** | PNG spritesheet | 128×192, 32×48 cells (4 directions, variants) |
| **Items** | PNG spritesheet | 256×256, 32×32 cells (8×8 grid, 64 items) |
| **Tools** | PNG spritesheet | 160×32, 32×32 cells (5 tools) |
| **Buildings** | Individual PNGs | Transparent backgrounds |
| **Backgrounds** | Individual PNGs | Zone-specific artwork |
| **UI Elements** | Individual PNGs | Buttons, frames, icons |

**Asset loading:** Custom AssetManager with JSON manifest and pre-caching.

---

## PWA Support

| Feature | Implementation |
|---------|---------------|
| **Service Worker** | `sw.js` — offline caching of game assets |
| **Web Manifest** | `manifest.json` — installable on desktop/mobile |
| **Offline Play** | Full game playable without internet after first load |

---

## Data Architecture

| Data Type | Storage | Description |
|-----------|---------|-------------|
| **Game Config** | JSON files | Quest definitions, NPC data, item properties, building specs |
| **Runtime State** | JavaScript objects | In-memory game state during play |
| **Save Data** | localStorage (Base64) | Serialized game state snapshot |
| **Assets** | PNG + JSON manifest | Sprites, backgrounds, UI elements |

---

## What's NOT in the Stack

This is as notable as what IS in the stack:

| Omitted | Why It's Impressive |
|---------|-------------------|
| **No game engine** (Unity, Godot, Phaser) | Every system built from first principles |
| **No UI framework** (React, Vue) | All UI rendered on Canvas |
| **No build tools** (webpack, vite, rollup) | Native ES6 modules load directly |
| **No package manager** (npm, yarn) | Zero dependencies |
| **No transpiler** (Babel, TypeScript) | Vanilla JavaScript runs as-is |
| **No database** | localStorage for persistence |
| **No server** | 100% client-side |

---

*© 2024-2026 DevynAi. All rights reserved.*
