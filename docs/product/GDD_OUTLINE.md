# Game Design Document — Desktop Garden (Outline)

| | |
| --- | --- |
| **Title** | Desktop Garden (working) |
| **Genre** | Desktop idle / living ecosystem sim |
| **Platform** | Windows 11 (primary), Unity 6 LTS |
| **Target** | Steam commercial |
| **GDD version** | 0.1 — outline for review |
| **Full GDD target size** | 300–500 pages equivalent (multi-volume, not single file) |
| **Vision** | `DESKTOP_GARDEN_VISION.md` |
| **Technical architecture** | `DESKTOP_IDLE_SIM_ARCHITECTURE.md` |
| **Delivery plan** | `GAME_MASTER_PLAN.md` |

---

## How to read this document

- **Part I–III** below are **written** (design intent).  
- **Part IV–X** are **table of contents** — each chapter expands in future volumes (`GDD_VOL_02_SYSTEMS.md`, etc.) after you approve vision + tier.  
- Page estimates assume printed A4; digital sections may be shorter/longer.

---

# Part I — Executive Summary (≈15 pages equivalent)

## 1.1 High concept

Desktop Garden turns the Windows desktop into a **persistent micro-ecosystem**: mushrooms and garden life grow with **moisture**, **weather**, **seasons**, and **celestial cycles**; the player tends the garden in short sessions while the world runs lightly in the background.

## 1.2 Design pillars

1. **Respect the OS** — low CPU/GPU, no focus steal, optional wallpaper mode.  
2. **Water matters** — moisture simulation is core, not cosmetic.  
3. **Living sky** — time-of-day, moon, rare events change play opportunities.  
4. **Data, not code** — species, mutations, shop, events ship as content.  
5. **Identity** — ecosystem + mutations + celestial hooks, not a reskin.

## 1.3 Reference competitor (learn, don’t clone)

| Source | Takeaway for us |
| --- | --- |
| Mushroom Nook (Steam listing) | Loop: grow, touch, collect, decorate; scale of species; cozy tone |
| Our addition | Humidity, weather gameplay, fauna AI, moon/mutation, multi-biome |

## 1.4 Success metrics (Steam)

- Median session 5–15 min; D1 retention target TBD after beta.  
- Wishlist conversion; review sentiment on performance & cozy depth.  
- Crash-free sessions > 99% beta.

## 1.5 Scope tiers (ship strategy)

See `DESKTOP_GARDEN_VISION.md` §5 — Tier A (VS1) → D (full 250+ species).

---

# Part II — Player Experience (≈40 pages equivalent)

## 2.1 Personas

- **Ambient worker** — game visible while coding; minimal clicks.  
- **Collector** — bestiary, rarity, mutations.  
- **Decorator** — layout expression.  
- **Completionist** — achievements, seasons, events.

## 2.2 Core loop (detailed)

```text
Observe → Assess moisture/weather → Water/Harvest → Spend/Shop →
Place decor → Log progress (bestiary) → Leave (offline accrual capped)
```

## 2.3 Session types

| Session | Duration | Actions |
| --- | --- | --- |
| Glance | 0–30 s | None / admire |
| Tend | 2–5 min | Water, harvest |
| Deep | 15+ min | Shop, decor, collection |

## 2.4 First-time user experience (FTUE)

Chapters to expand (Vol UX):

- Install → bootstrap → first plot unlocked  
- Tool: watering can → moisture bar tutorial  
- First harvest → inventory → shop tease  
- Optional: desktop mode unlock after windowed comfort (Tier B)

## 2.5 Progression philosophy

No hard combat; **mastery** via collection, garden rating (optional), unlock tree — avoid mandatory daily grind for Tier A/B.

---

# Part III — Systems Catalog (≈60 pages equivalent)

Each system: **Purpose | Player-visible | Data | Dependencies | Tier**

## 3.1 Desktop & platform

| System | Tier | Notes |
| --- | --- | --- |
| Transparent window | B | URP alpha |
| Click-through + hit islands | B | `HitTestManager` |
| Multi-monitor / DPI | B | |
| Tray / single-instance | B | |
| Boot with Windows | C | Opt-in |

## 3.2 Time & celestial

| System | Tier | Notes |
| --- | --- | --- |
| Time-of-day (7 phases) | B simplified, C full | Color + audio |
| Season (4) | B | Growth tables |
| Moon phase (8) | C | Spawn/mutation |
| Sun arc / grading | C | Visual |
| Rare sky events | D | Eclipse, meteor, aurora |

## 3.3 Environment

| System | Tier | Notes |
| --- | --- | --- |
| Weather FSM | B | Sunny, rain, snow, fog, wind |
| Temperature (region) | C | Biome default |
| Per-plot moisture | A | **Core** |
| Water types | C | Items |

## 3.4 Flora (mushrooms & plants)

| System | Tier | Notes |
| --- | --- | --- |
| Species definitions | A | SO + Addressables |
| Growth stages | A | Through dead/recycle |
| Wilt / recovery | A | Moisture linked |
| Mutation recipes | C | Data-driven |
| Rarity tiers | B→D | 250+ target |

## 3.5 Fauna

| System | Tier | Notes |
| --- | --- | --- |
| Fauna spawn schedules | C | Day/night |
| AI state machine | C | Shared library |
| Interact pet/feed | D | Optional |

## 3.6 Interaction verbs

| Verb | Tier | Command |
| --- | --- | --- |
| Water | A | `WaterPlotCommand` |
| Harvest | A | `HarvestCommand` |
| Inspect | B | `InspectCommand` |
| Move/Sell/Destroy | B/C | |
| Pet | D | |
| Photo | C | Photo mode |

## 3.7 Decoration & world

| System | Tier | Notes |
| --- | --- | --- |
| Grid placement | C | DEC-01 |
| Biome backgrounds | B | Parallax layers |
| Particles | B | Weather-linked |

## 3.8 Economy & metagame

| System | Tier | Notes |
| --- | --- | --- |
| Soft currency | B | |
| Multi-wallet | C/D | Enable gradually |
| Shop rotations | B | Daily/season |
| Achievements | C | Local → Steam |
| Quests/dailies | C | Cap scope |
| Bestiary | C | |

## 3.9 Persistence & platform

| System | Tier | Notes |
| --- | --- | --- |
| JSON save + migrator | A | |
| Backup/export | C | |
| Steam + cloud | D | Optional cloud |

## 3.10 Audio & UI

Cross-ref modules 19–20 in vision doc; per-screen specs in **Part VI (TOC)**.

---

# Part IV — Content Bible (TOC, ≈80 pages)

## 4.1 Mushroom taxonomy

- Families, biomes, rarity tables  
- 250+ row schema (spreadsheet → ScriptableObject pipeline)  
- Seasonal & event columns  

## 4.2 Mutation compendium

- Recipe format: inputs (species, weather, moon, item) → output  
- Balance rules: pity, cooldown, once-per-save flags  

## 4.3 Decoration catalog

- 200 items: footprint, theme, unlock  

## 4.4 Fauna catalog

- 80 species max target; behavior profiles  

## 4.5 Biomes & backgrounds

- Forest, garden, snow, desert, fantasy, night, rain, lake, mountain — layer spec (sky, cloud, ground, light)  

## 4.6 Items & tools

- Watering cans, food, tickets, skins  

## 4.7 Shop tables

- Daily/weekly/season/event/legendary — weight formulas  

## 4.8 Live ops events

- Eclipse week, cherry blossom, lantern festival templates  

---

# Part V — Technical Design (TOC, ≈50 pages)

> **Source of truth for implementation:** `DESKTOP_IDLE_SIM_ARCHITECTURE.md`

## 5.1 Layer diagram & asmdef

## 5.2 Service / system registry (not Manager list)

## 5.3 Event bus catalog (all game events)

## 5.4 Save schema versions (v1…vn)

## 5.5 Addressables labeling strategy

## 5.6 Win32 desktop integration

## 5.7 Performance budgets per tier

## 5.8 UML / class diagrams (per volume)

- Domain model  
- Command flow  
- UI MVVM  

## 5.9 ScriptableObject field dictionary

- `SpeciesDefinition`  
- `MutationRecipe`  
- `WeatherProfile`  
- `ShopOfferTable`  
- `FaunaDefinition`  
- `BiomeDefinition`  

## 5.10 Anti-cheat / save integrity

Checksum, optional encryption; no kernel drivers.

---

# Part VI — UI / UX Specification (TOC, ≈70 pages)

Per screen: **wireframe | states | navigation | data bindings | accessibility**

## 6.1 Global HUD

## 6.2 Inventory

## 6.3 Collection / Bestiary

## 6.4 Shop (tabs: daily, weekly, season, event, legendary)

## 6.5 Map / biome picker

## 6.6 Quest journal

## 6.7 Achievements

## 6.8 Photo mode

## 6.9 Settings (graphics, sim, desktop, audio, privacy, language)

## 6.10 Save / load / export

## 6.11 Tooltips & notifications

## 6.12 Modal flows (sell, destroy confirm)

## 6.13 Desktop interaction mode indicator

---

# Part VII — Art & Animation (TOC, ≈60 pages)

## 7.1 Style guide (pixel scale, palette, lighting)

## 7.2 Sprite naming & atlas rules

## 7.3 Mushroom stage art matrix

## 7.4 Animation library (idle, wind, happy, grow, collect, sleep, rain, night, legendary…)

## 7.5 VFX particles catalog

## 7.6 UI art kit

## 7.7 Background parallax spec

## 7.8 Animal animation sets

## 7.9 Seasonal recolor tables

---

# Part VIII — Audio Design (TOC, ≈25 pages)

## 8.1 Bus structure

## 8.2 Ambient layers per time/weather/biome

## 8.3 SFX list (water, harvest, UI, footsteps, creatures)

## 8.4 Music stingers & rare events

## 8.5 Mixing rules for desktop (low intrusion)

---

# Part IX — Balance & Economy (TOC, ≈40 pages)

## 9.1 Growth time curves

## 9.2 Moisture decay rates

## 9.3 Offline accrual caps

## 9.4 Currency faucets & sinks

## 9.5 Shop pricing & rotation

## 9.6 Mutation rates & protection

## 9.7 Rarity distribution

## 9.8 Playtest telemetry hooks (opt-in)

---

# Part X — Production (TOC, ≈40 pages)

## 10.1 Team roles (solo vs studio)

## 10.2 Sprint breakdown (2-week sprints → stories)

## 10.3 Milestone mapping (GAME_MASTER_PLAN)

## 10.4 Risk register

## 10.5 QA matrices (Win11 desktop, save, economy)

## 10.6 Steam release checklist

## 10.7 Post-launch content cadence (season packs)

## 10.8 Mod support roadmap (post-1.0)

---

# Appendix A — Module 1–25 quick index

Maps user’s 25 modules to Part III–VII (see `DESKTOP_GARDEN_VISION.md` §6).

# Appendix B — Manager name → Service mapping

See `DESKTOP_GARDEN_VISION.md` §7.

# Appendix C — Competitive feature matrix

Expand with other desktop pets / idle garden titles as research proceeds.

# Appendix D — Glossary

Moisture, wilt, mutation, phase, tier, plot, spore, wallet, rotation seed.

---

# Volume delivery plan (after vision approve)

| Volume | File (future) | Est. pages | Priority |
| --- | --- | --- | --- |
| 1 | `GDD_VOL_01_EXPERIENCE.md` | 40 | P1 |
| 2 | `GDD_VOL_02_SYSTEMS_DEEP.md` | 60 | P1 |
| 3 | `GDD_VOL_03_CONTENT_SCHEMA.md` | 80 | P2 |
| 4 | `GDD_VOL_04_UI_UX.md` | 70 | P2 |
| 5 | `GDD_VOL_05_ART_ANIM.md` | 60 | P3 |
| 6 | `GDD_VOL_06_BALANCE.md` | 40 | P2 |
| 7 | `GDD_VOL_07_PRODUCTION.md` | 40 | P1 |

**Total path to 300+:** Volumes 1–7 + architecture + master plan appendices.

---

# Sprint-ready breakdown (preview)

Aligns with `GAME_MASTER_PLAN` stories; **Tier A** first 16 sprints sketch:

| Sprint | Goal |
| --- | --- |
| S1 | P0 + US-M0-01–03 |
| S2 | US-M0-04–09 |
| S3 | US-M2-01–03 + moisture model design lock |
| S4 | US-M2-04–07 |
| S5 | US-M2-08–09 + water verb design |
| S6 | US-M3-01–04 |
| S7 | US-M3-05–10 **VS1** |
| S8+ | Tier B per master plan |

Full sprint table expands in Vol 7 after tier lock (V3).

---

*GDD Outline v0.1 — review with `DESKTOP_GARDEN_VISION.md`. Approve vision + tier before writing Vol 1–7.*