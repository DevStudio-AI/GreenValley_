# Green Valley — Security

> Security considerations for a client-side browser game

---

## Threat Model

Green Valley is a **single-player, client-side web game** with no server, no accounts, and no network communication during gameplay. The threat model is fundamentally different from a web application.

| Factor | Status |
|--------|--------|
| **Server-side attack surface** | None — no backend |
| **User accounts / credentials** | None |
| **Payment processing** | None |
| **User-generated content** | None |
| **Multiplayer / network play** | None |
| **External API calls** | None |

---

## Client-Side Protections

### Save Data Integrity

```
localStorage → JSON.stringify(gameState) → Base64 encode → store
                                                              ↓
load → Base64 decode → JSON.parse() → validate → restore gameState
```

| Check | Implementation |
|-------|---------------|
| **Deserialization** | `JSON.parse()` wrapped in try/catch |
| **Schema validation** | Required fields checked before state restore |
| **Corrupt data handling** | Falls back to new game if save is invalid |
| **Version migration** | Save format includes version marker |

### Input Validation

| Layer | What's Checked |
|-------|---------------|
| **Key events** | Only mapped keys trigger actions |
| **Tool actions** | Tool must be equipped and player within range |
| **Inventory operations** | Quantity checks, stack limits enforced |
| **NPC interactions** | Proximity and state validation |
| **Quest completion** | Requirement fulfillment verified in-memory |

### Game State Boundaries

| Boundary | Enforcement |
|----------|------------|
| **Player position** | Clamped to zone bounds |
| **Resource values** | Min/max enforced (energy: 0–max, gold: 0+) |
| **Time progression** | Validated ticks, no negative time |
| **Inventory slots** | Fixed capacity, overflow rejected |
| **Relationship range** | 0–300+ with tier thresholds |

---

## PWA & Service Worker Security

| Measure | Implementation |
|---------|---------------|
| **Cache scope** | Service worker only caches own-origin assets |
| **Update strategy** | Cache-first with network fallback |
| **No external fetches** | All assets bundled — no CDN, no third-party scripts |
| **Content Security Policy** | Recommended: `default-src 'self'` |

---

## Supply Chain

| Category | Detail |
|----------|--------|
| **Dependencies** | **Zero** — no npm packages, no external libraries |
| **CDN usage** | None — all assets served from same origin |
| **Third-party scripts** | None |
| **Build pipeline** | None — no opportunity for build-time injection |

Zero dependencies means zero supply-chain attack surface.

---

## Privacy

| Category | Detail |
|----------|--------|
| **Data collected** | None |
| **Analytics** | None |
| **Cookies** | None |
| **Network requests** | None during gameplay |
| **Storage** | localStorage only — never leaves the browser |

---

## Content Security

| Measure | Implementation |
|---------|---------------|
| **No `eval()`** | All code is static — no dynamic code execution |
| **No `innerHTML` mutations** | UI rendered on Canvas, not DOM |
| **No user text injection** | All displayed text comes from game config files |
| **Asset loading** | Images loaded via `Image()` constructor with `onload`/`onerror` |

---

## Recommended Deployment Headers

For serving the game on a web host:

```
Content-Security-Policy: default-src 'self'; img-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: no-referrer
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

---

*© 2024-2026 DevynAi. All rights reserved.*
