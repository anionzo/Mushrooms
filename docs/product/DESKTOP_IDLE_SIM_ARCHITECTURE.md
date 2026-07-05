# Desktop Idle Ecosystem Simulation — System Architecture

**Status:** Architecture baseline (no implementation)  
**Stack:** Windows 11, Unity 6 LTS, C#, URP 2D, Git, JSON save, Addressables, ScriptableObjects, Win32 desktop integration  
**Product codename:** Desktop Mushroom Ecosystem (working title; not a clone of any specific title)

---

## 1. Product Vision

### Goal

Deliver a **commercial-quality desktop idle simulation** that lives on the user’s Windows desktop as a **low-footprint, always-on ecosystem**. The player cultivates mushrooms, decorates a micro-habitat, and progresses through economy and collection loops **without demanding active attention**, while still offering satisfying moments of interaction, discovery, and expression.

**Why:** Desktop “companion” games succeed when they respect the OS (CPU/GPU, focus, input) and reward long horizons. Architecture must optimize for **continuous simulation at variable tick rates**, **modular content**, and **years of live updates**.

### Core Loop

1. **Observe** — glancing at growth, weather, and visitors on the desktop layer.  
2. **Tend** — occasional watering, placement, harvest, shop purchases.  
3. **Progress** — currency, unlocks, achievements, journal/photo collection.  
4. **Express** — decorations, layouts, photo mode, seasonal themes.  
5. **Return** — offline/idle accrual, events, new species/biomes via content drops.

### Long-Term Gameplay

- Deep **species catalog** with rarity, synergies, and biome affinity.  
- **Seasons and weather** altering growth curves and visuals.  
- **Meta progression** (tools, greenhouse upgrades, automation helpers) without mandatory grinding.  
- **Collection and narrative fragments** (field guide, NPC mail, environmental storytelling).  
- **Live ops hooks** (limited events, rotating shop, daily/weekly goals) optional for commercial phase.

### Expansion Possibilities

| Horizon | Examples |
| --- | --- |
| Content | New biomes, pets, NPC schedules, mushroom mutations, hybrid breeding |
| Platform | Steam achievements/workshop, cloud save, companion mobile “check-in” app |
| Social | Asynchronous visits, gift spores, shared garden snapshots (non-real-time) |
| Tech | Mod pipeline, scripted events, procedural decoration packs |
| Business | DLC biomes, cosmetic battle pass–style seasons (if aligned with product ethics) |

---

## 2. Functional Requirements

### Desktop & Window

| ID | Feature | Description |
| --- | --- | --- |
| DW-01 | Desktop window mode | Borderless, transparent-capable render target over desktop |
| DW-02 | Window layering | Configurable: above icons / below windows / “wallpaper-like” |
| DW-03 | Click-through | Pass mouse to desktop except on interactive hit targets |
| DW-04 | Multi-monitor | Per-display placement, DPI-aware bounds, restore on reconnect |
| DW-05 | Focus policy | No focus steal; optional “interaction mode” with temporary focus |
| DW-06 | Tray / background | Minimize-to-tray; run when no visible game window (simulation continues) |
| DW-07 | Startup | Boot with Windows (opt-in), safe single-instance lock |
| DW-08 | Resolution & scale | Logical UI scale independent of desktop resolution |

### Simulation & Mushrooms

| ID | Feature |
| --- | --- |
| SIM-01 | Real-time and accelerated time modes |
| SIM-02 | Mushroom life cycle: spore → growth stages → harvest → decay (optional) |
| SIM-03 | Substrate/plot slots with capacity and adjacency rules |
| SIM-04 | Growth modifiers: water, nutrients, light, temperature, species traits |
| SIM-05 | Offline progression with caps and fairness rules |
| SIM-06 | Ecosystem ambience: insects, particles, ambient audio layers |
| SIM-07 | Rare spawns and discovery moments |

### Decoration & World

| ID | Feature |
| --- | --- |
| DEC-01 | Place/move/rotate decorations with grid or free placement modes |
| DEC-02 | Layering (background, mid, foreground) and z-order |
| DEC-03 | Collision / occupancy for plots and paths |
| DEC-04 | Themed sets (seasonal, event, shop exclusives) |
| DEC-05 | Undo/redo for placement sessions (session-local) |

### Inventory & Items

| ID | Feature |
| --- | --- |
| INV-01 | Item types: spores, harvest, tools, consumables, cosmetics, blueprints |
| INV-02 | Stack rules, rarity, binding flags (soulbound cosmetics) |
| INV-03 | Sort/filter, quick-use from HUD |
| INV-04 | Item definitions data-driven (ScriptableObjects + Addressables) |

### Economy & Shop

| ID | Feature |
| --- | --- |
| ECO-01 | Soft currency earn/spend sinks and sources |
| ECO-02 | Shop rotations, bundles, pity/rarity transparency (regional compliance later) |
| ECO-03 | Crafting (optional milestone): combine harvest → products |
| ECO-04 | Price curves and inflation control via simulation telemetry hooks |

### Weather & Seasons

| ID | Feature |
| --- | --- |
| WTH-01 | Weather states with blended transitions |
| WTH-02 | Season calendar affecting growth tables and visuals |
| WTH-03 | Player-toggle “follow real-world season” vs in-game calendar |

### Particles & VFX

| ID | Feature |
| --- | --- |
| VFX-01 | Pooled particle systems (rain, spores, fireflies) |
| VFX-02 | Quality presets tied to performance profile |
| VFX-03 | Photo mode: hide UI, freeze time, filters |

### Progression

| ID | Feature |
| --- | --- |
| PRG-01 | Player level / mastery (non-combat) |
| PRG-02 | Unlock tree for species, decorations, biomes |
| PRG-03 | Achievements (local + Steam when integrated) |
| PRG-04 | Quests / dailies / guided tutorials |
| PRG-05 | Field guide completion rewards |

### Interaction & Input

| ID | Feature |
| --- | --- |
| INP-01 | Mouse-first; optional hotkeys |
| INP-02 | Tool modes: inspect, harvest, place, photo |
| INP-03 | Context menus on entities |
| INP-04 | Accessibility: UI scale, reduce motion, color-blind patterns |

### Audio

| ID | Feature |
| --- | --- |
| AUD-01 | Layered ambient loops with crossfade |
| AUD-02 | SFX bus with pooling; mute categories independently |
| AUD-03 | Music stingers for rare events |

### UI

| ID | Feature |
| --- | --- |
| UI-01 | HUD minimal by default; expand on hover/hotkey |
| UI-02 | Windows: inventory, shop, settings, journal, map/biome picker |
| UI-03 | Notifications queue (non-blocking) |
| UI-04 | Tooltips with data-driven content |
| UI-05 | Modal dialogs for destructive actions |

### Settings

| ID | Feature |
| --- | --- |
| SET-01 | Graphics: quality, FPS cap, VSync, particle density |
| SET-02 | Simulation: tick rate when focused/unfocused |
| SET-03 | Desktop: layer, click-through default, monitor selection |
| SET-04 | Audio volumes, language |
| SET-05 | Privacy: analytics opt-in, crash reports |

### Localization

| ID | Feature |
| --- | --- |
| L10N-01 | String tables + asset variants where needed |
| L10N-02 | Font fallbacks per locale |
| L10N-03 | RTL readiness in UI layout architecture (future) |

### Save & Persistence

| ID | Feature |
| --- | --- |
| SAV-01 | Autosave on interval and on critical events |
| SAV-02 | Manual save slots (at least 3) |
| SAV-03 | Export/import for backup |
| SAV-04 | Save versioning and migration |

### Platform Integrations (phased)

| ID | Feature |
| --- | --- |
| PLT-01 | Steam: overlay-safe input, achievements, cloud (optional) |
| PLT-02 | Crash reporting (e.g. Backtrace / Sentry-style) |
| PLT-03 | Update channel: stable / beta |

### Mod Support (future-ready)

| ID | Feature |
| --- | --- |
| MOD-01 | Load order for JSON + Addressable-like local packs |
| MOD-02 | Signature / sandbox rules for untrusted mods |
| MOD-03 | In-game mod manager UI |

### Developer / Ops (non-player)

| ID | Feature |
| --- | --- |
| OPS-01 | In-editor simulation fast-forward |
| OPS-02 | Cheat/debug menu (dev builds only) |
| OPS-03 | Structured logging and log levels |
| OPS-04 | Feature flags for staged rollout |

---

## 3. Non-Functional Requirements

### Performance

| Metric | Target (commercial) | Rationale |
| --- | --- | --- |
| CPU (idle desktop) | < 2–5% of one core on mid-range laptop | Wallpaper apps must not throttle battery |
| CPU (active interaction) | < 15% one core sustained | Headroom for spikes |
| GPU | Minimal when scene static; batch-friendly 2D | URP 2D + atlasing |
| Frame rate | 30 FPS cap option when unfocused; 60 when interacting | User-configurable |
| Simulation tick | 1–10 Hz unfocused; up to 30 Hz focused | Decouple sim from render |

### Memory

- Working set **< 500 MB** typical; **< 1 GB** with large Addressables cache.  
- Pool all transient gameplay objects; avoid per-frame allocations in hot paths.

### Architecture Quality

- **Modular bounded contexts** (Growth, Economy, Desktop, UI) with explicit contracts.  
- **No god singleton**; use scoped services and composition roots.  
- **Testability:** domain logic pure C# where possible (asmdef `*.Core`).

### Maintainability & Scalability

- New mushroom species = **data + art**, not code changes.  
- New shop season = **content pack** + optional scriptable event graph.  
- Horizontal scaling of content via Addressables labels.

### Security

- Save files: checksum + optional encryption for tamper resistance (not anti-cheat).  
- No elevated privileges; validate paths for mod/import.  
- Steam/cloud tokens never logged.

### Loading Time

- Cold start **< 8 s** on SSD (excluding first-time Addressables build).  
- Warm resume **< 2 s** from tray.

### Save System

- Atomic writes (temp file + rename).  
- Autosave must not block main thread > 16 ms; use background thread + main-thread apply.

### Error Handling

- Fail-soft for content load errors (placeholder + report).  
- Fail-hard for corrupt save with recovery UI (restore backup).

### Logging

- Categories: Sim, Save, Desktop, UI, Network, Mod.  
- Ring buffer in memory for support bundles; file rotation on disk.

---

## 4. High Level Architecture

### Layered Model

```text
┌─────────────────────────────────────────────────────────────────┐
│                    Presentation (Unity View)                     │
│  URP 2D Cameras, Animators, VFX, UI (UIToolkit + uGUI hybrid)   │
└───────────────────────────────┬─────────────────────────────────┘
                                │ binds to ViewModels / presenters
┌───────────────────────────────▼─────────────────────────────────┐
│                      Application / Gameplay                      │
│  Systems orchestration, commands, use-cases, session lifecycle   │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                         Domain / Core                            │
│  Rules: growth math, economy invariants, time, unlock logic      │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                        Infrastructure                            │
│  Save IO, Addressables, Audio, Input, Desktop Win32, Steam       │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                     Data & Configuration                         │
│  ScriptableObjects, JSON schemas, tables, localization           │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│              Platform (Windows 11, Unity Player, GPU)              │
└─────────────────────────────────────────────────────────────────┘
```

### Cross-Cutting

```text
        Event Bus ────────┬──────── State Machines
                          │
        Service Registry / DI Composition Root
                          │
        Utilities (math, time, pooling, logging)
```

### Dependency Rule

- **Core** has zero UnityEngine references (except optional `Unity.Mathematics`).  
- **Gameplay** references Core + abstractions (`ISaveService`, `IEventBus`).  
- **Infrastructure** implements abstractions; registered at bootstrap.  
- **Presentation** listens to events / ViewModels; never mutates save directly.

### Runtime Bootstrap Sequence

```text
AppEntry (scene) → PlatformCapabilities probe → Load Settings
  → CompositionRoot.Build() → Register Services
  → DesktopWindowHost.Initialize() → ContentCatalog.LoadAsync()
  → SaveCoordinator.LoadOrNew() → GameStateMachine → Enter Running
```

### Diagram: Simulation vs Render

```text
  ┌──────────────┐         ┌─────────────────┐
  │ SimScheduler │──tick──▶│ SimulationSystems│
  └──────────────┘         └────────┬────────┘
                                    │ events / dirty flags
  ┌──────────────┐         ┌────────▼────────┐
  │ Unity Loop   │──render▶│ View Sync Layer │
  └──────────────┘         └─────────────────┘
```

**Why:** Decoupling allows low-frequency simulation when the desktop is click-through and static.

---

## 5. Folder Structure

Unity project root (game repo separate from harness docs repo recommended; structure below is canonical game layout).

```text
MushroomDesktop/
├── .gitignore
├── Packages/
│   └── manifest.json
├── ProjectSettings/
├── Assets/
│   ├── _Game/                          # All first-party game content
│   │   ├── Scenes/
│   │   │   ├── Bootstrap.unity
│   │   │   ├── DesktopPlay.unity
│   │   │   └── DevTest.unity
│   │   ├── Prefabs/
│   │   │   ├── Mushrooms/
│   │   │   ├── Decorations/
│   │   │   ├── UI/
│   │   │   └── VFX/
│   │   ├── Art/
│   │   │   ├── Sprites/
│   │   │   ├── Atlases/
│   │   │   ├── Materials/
│   │   │   └── Shaders/
│   │   ├── Audio/
│   │   │   ├── Music/
│   │   │   ├── SFX/
│   │   │   └── Mixers/
│   │   ├── Animation/
│   │   ├── Data/                       # ScriptableObject assets
│   │   │   ├── Species/
│   │   │   ├── Items/
│   │   │   ├── Shop/
│   │   │   ├── Weather/
│   │   │   ├── Quests/
│   │   │   └── Tuning/
│   │   ├── Localization/
│   │   │   ├── Tables/
│   │   │   └── Locales/
│   │   ├── UI/
│   │   │   ├── UXML/
│   │   │   ├── USS/
│   │   │   └── Sprites/
│   │   └── AddressableAssetsData/
│   ├── Plugins/
│   │   ├── Windows/
│   │   │   └── DesktopIntegration/     # Win32 P/Invoke layer
│   │   └── Steam/                      # Steamworks.NET (when used)
│   ├── Resources/                      # Minimal bootstrap only
│   │   └── AppConfig.asset
│   ├── StreamingAssets/
│   │   ├── DefaultSave/
│   │   └── Mods/
│   └── ThirdParty/
├── Packages/com.company.mushroom.core/ # Optional UPM local packages
├── Tests/
│   ├── EditMode/
│   │   └── Mushroom.Core.Tests/
│   └── PlayMode/
│       └── Mushroom.Integration.Tests/
├── Tools/
│   ├── Build/
│   ├── SaveMigrator/
│   └── ContentValidators/
└── Docs/
    ├── Architecture/
    └── ContentAuthoring/
```

### Assembly Definition Map

| Assembly | Role |
| --- | --- |
| `Mushroom.Core` | Domain, pure logic |
| `Mushroom.Core.Contracts` | Interfaces, DTOs, event contracts |
| `Mushroom.Gameplay` | Systems, state machines, use cases |
| `Mushroom.Infrastructure` | Save, Addressables, platform |
| `Mushroom.Presentation` | MonoBehaviours, views, presenters |
| `Mushroom.Editor` | Validators, tooling |
| `Mushroom.Desktop.Win32` | Window hooks (isolated for security review) |

**Why asmdefs:** Enforce dependency direction and faster compile/test cycles.

---

## 6. Software Architecture

### Composition Root & DI

- **Pattern:** Constructor injection via a lightweight **ServiceRegistry** built at bootstrap (Zenject/ VContainer optional; custom acceptable if boundaries stay clear).  
- **Why:** Testability and explicit lifetimes (Singleton vs Scene vs Transient).

### Service Locator

- **Avoid** except for legacy Unity entry points; if used, thin facade over registry for `MonoBehaviour` bridges only.

### Managers (Anti-Pattern Guardrails)

| Allowed | Forbidden |
| --- | --- |
| `AudioService`, `SaveCoordinator` as **services** | `GameManager` owning 50 responsibilities |
| Facade coordinators with **delegation** | Static mutable global state for gameplay rules |

### Systems

- **ISimulationSystem** with `OnTick(SimContext)`, ordered by **SystemPipeline** configuration (ScriptableObject).  
- **Why:** Add WeatherSystem without editing GrowthSystem.

### Controllers

- **InputController** translates raw input → **Commands** (`HarvestCommand`, `PlaceDecorationCommand`).  
- **Why:** Command pattern enables undo, replay, and network sync later.

### Factories

- `IMushroomViewFactory`, `IItemInstanceFactory` — spawn runtime entities from definitions + save state.  
- **Why:** Centralize pooling and Addressable handles.

### Repositories

- `ISaveRepository`, `IPlayerProfileRepository`, `IContentCatalog` — abstract persistence and content lookup.  
- **Why:** Swap JSON for SQLite cloud cache later without touching gameplay.

### Models

- **Definition models** (immutable SO-backed): `SpeciesDefinition`, `ItemDefinition`.  
- **Runtime models** (mutable): `MushroomInstance`, `PlotState`, `PlayerWallet`.  
- **Save models** (serializable DTOs): versioned, no Unity references.

### Event Bus

- **Typed events** `IEventBus.Publish<T>()` / `Subscribe<T>()` with weak disposal for UI.  
- **Why:** UI and achievements react without polling.

### Observer

- Use for **view binding** (ViewModel implements `INotifyPropertyChanged` or Unity-specific reactive wrapper).

### State Machines

- **GameStateMachine:** Boot → Loading → Playing → Paused → ShuttingDown.  
- **Per-entity:** Mushroom growth states, UI modal stack.  
- **Library:** Optional `Stateful` base or Unity `Playables` only for animation—not for core rules.

### Strategy Pattern

- `IGrowthCurveStrategy`, `IPricingStrategy`, `IOfflineAccrualPolicy` selected by species/season data.  
- **Why:** Balance tuning without subclass explosion.

### Data-Driven Design

- Designers own curves in SO; engineers own pipelines and validators.

### Composition over Inheritance

- Mushroom behavior = **components** (`GrowthComponent`, `HarvestableComponent`) assembled from definition.

### Singletons

- Only **AppLifetime** token and **Logging**—everything else scoped.

---

## 7. Gameplay Systems

For each: **Purpose | Inputs | Outputs | Dependencies | Future Expansion**

### Time System

| | |
| --- | --- |
| **Purpose** | Authoritative simulation clock, pause, scale, offline delta |
| **Inputs** | Real time, focus state, settings (tick rate) |
| **Outputs** | `SimTick`, `GameDay`, `SeasonPhase` events |
| **Dependencies** | Save (last timestamp), Settings |
| **Expansion** | Scheduled world events, real-time sync seasons |

### Growth System

| | |
| --- | --- |
| **Purpose** | Advance mushroom stages from environmental inputs |
| **Inputs** | Plot state, weather, water level, species defs |
| **Outputs** | Stage transitions, harvest readiness, death/decay |
| **Dependencies** | Time, Weather, Inventory (nutrients) |
| **Expansion** | Mutations, symbiosis with decorations |

### Spawn System

| | |
| --- | --- |
| **Purpose** | Introduce spores, ambient creatures, particles |
| **Inputs** | Biome rules, player actions, RNG streams |
| **Outputs** | New instances, VFX triggers |
| **Dependencies** | Growth, Economy (cost), Content catalog |
| **Expansion** | Invasive species events, rare hunts |

### Season System

| | |
| --- | --- |
| **Purpose** | Calendar boundaries affecting tables and art |
| **Inputs** | Time, optional real-world calendar |
| **Outputs** | `SeasonChanged`, modifier application |
| **Dependencies** | Time, Weather |
| **Expansion** | Hemisphere toggle, player-hosted “festivals” |

### Weather System

| | |
| --- | --- |
| **Purpose** | Active weather state and transitions |
| **Inputs** | Season, biome, random tables |
| **Outputs** | Growth modifiers, shader params, audio layers |
| **Dependencies** | Time, Season, Presentation (VFX) |
| **Expansion** | Extreme weather disasters (soft penalties) |

### Economy System

| | |
| --- | --- |
| **Purpose** | Wallets, transactions, sinks/sources audit |
| **Inputs** | Commands (purchase, sell, reward) |
| **Outputs** | Balance changes, transaction log events |
| **Dependencies** | Inventory, Shop catalog, Save |
| **Expansion** | Multi-currency, player market (async) |

### Inventory System

| | |
| --- | --- |
| **Purpose** | Own items, stacks, equip/use |
| **Inputs** | Pickup, harvest, shop grants |
| **Outputs** | Item added/removed events |
| **Dependencies** | Economy, Content defs |
| **Expansion** | Loadouts, auto-sort rules |

### Shop System

| | |
| --- | --- |
| **Purpose** | Present offers, execute purchases |
| **Inputs** | Shop tables, player level, rotation seed |
| **Outputs** | Inventory grants, currency spend |
| **Dependencies** | Economy, Inventory, Time |
| **Expansion** | Live ops remote catalog |

### Decoration System

| | |
| --- | --- |
| **Purpose** | Placement, validation, persistence |
| **Inputs** | Placement commands, grid rules |
| **Outputs** | Scene layout state, occupancy map |
| **Dependencies** | Save, Input, Camera |
| **Expansion** | Blueprint sharing, height layers |

### Interaction System

| | |
| --- | --- |
| **Purpose** | Raycast/hit targets, tool modes |
| **Inputs** | Desktop input (respect click-through) |
| **Outputs** | Focused entity, context actions |
| **Dependencies** | Input, Window hit-test layer |
| **Expansion** | Touch, gamepad |

### Collectibles & Field Guide

| | |
| --- | --- |
| **Purpose** | Discovery tracking, lore unlocks |
| **Inputs** | First-time events (species seen, harvested) |
| **Outputs** | Guide entries, achievement progress |
| **Dependencies** | Growth, Save |
| **Expansion** | AR photo challenges |

### Achievement System

| | |
| --- | --- |
| **Purpose** | Local + platform achievement unlock |
| **Inputs** | Event bus hooks |
| **Outputs** | Platform API calls, UI toast |
| **Dependencies** | Save, Steam adapter |
| **Expansion** | Hidden achievements, streaks |

### Quest System

| | |
| --- | --- |
| **Purpose** | Guided goals and dailies |
| **Inputs** | Quest defs, event progress |
| **Outputs** | Rewards, narrative beats |
| **Dependencies** | Economy, Inventory, Time |
| **Expansion** | Branching quest graphs |

### Unlock System

| | |
| --- | --- |
| **Purpose** | Gates content by level, achievements, items |
| **Inputs** | Player profile state |
| **Outputs** | `ContentUnlocked` events |
| **Dependencies** | Save, all progression sources |
| **Expansion** | Season pass tracks |

### Save System (Gameplay Facade)

| | |
| --- | --- |
| **Purpose** | Orchestrate dirty tracking and snapshots |
| **Inputs** | System dirty flags, manual save |
| **Outputs** | Persisted DTO |
| **Dependencies** | Infrastructure save IO |
| **Expansion** | Cloud merge |

### Camera System

| | |
| --- | --- |
| **Purpose** | Pan/zoom desktop scene, photo mode |
| **Inputs** | Input, constraints |
| **Outputs** | View matrix, screenshot capture |
| **Dependencies** | Presentation |
| **Expansion** | Cinematic tours |

### Animation System

| | |
| --- | --- |
| **Purpose** | Drive sprite animation from state |
| **Inputs** | Growth stage, weather |
| **Outputs** | Animator params |
| **Dependencies** | Presentation pools |
| **Expansion** | Procedural sway |

### Audio System

| | |
| --- | --- |
| **Purpose** | Bus mixing, adaptive ambient |
| **Inputs** | Weather, time of day, UI state |
| **Outputs** | Audio playback |
| **Dependencies** | Infrastructure audio |
| **Expansion** | User-imported playlists (policy) |

### UI System

| | |
| --- | --- |
| **Purpose** | Stack windows, HUD, modals |
| **Inputs** | Commands, events |
| **Outputs** | User commands |
| **Dependencies** | Input, Localization |
| **Expansion** | Widget skins |

### Desktop Integration System

| | |
| --- | --- |
| **Purpose** | Window layer, click-through, DPI |
| **Inputs** | Settings, focus mode |
| **Outputs** | Hit-test regions, Win32 state |
| **Dependencies** | Win32 plugin |
| **Expansion** | macOS layer (out of scope v1) |

---

## 8. Data Architecture

### ScriptableObjects (Authoring)

| Asset Type | Fields (conceptual) |
| --- | --- |
| `SpeciesDefinition` | id, growth curve ref, stages, harvest loot table, biome tags |
| `GrowthCurveDefinition` | stage durations, modifiers map |
| `ItemDefinition` | id, category, stack max, icon ref, use behavior id |
| `DecorationDefinition` | footprint, layers, unlock id |
| `ShopOfferTable` | entries, weights, rotation group |
| `WeatherProfile` | states, transition matrix |
| `QuestDefinition` | steps, conditions, rewards |
| `SystemPipelineConfig` | ordered system ids |

**Why SO:** Unity-native authoring, diff-friendly with YAML merge discipline.

### Runtime Objects

- `GameSession` — root aggregate referencing plots, entities, player profile.  
- `EntityId` — stable GUID per placed instance.  
- Pools reuse view objects; **state lives in session aggregate**.

### Save Objects (DTO)

```text
SaveFileV{n}
├── header: version, checksum, buildId, timestamp
├── player: currencies, unlocks, settings snapshot
├── world: plots[], mushrooms[], decorations[]
├── progression: quests, achievements, guide
└── meta: lastSimUtc, offlineCapApplied
```

### Configuration Objects

- `AppConfig` (Resources/bootstrap): feature flags, default quality.  
- `PlatformTuning` per OS/GPU tier.

### Addressables

| Label | Content |
| --- | --- |
| `core` | Bootstrap UI, essential species |
| `biome_{id}` | Biome bundles |
| `event_{id}` | Limited-time packs |
| `loc_{locale}` | Localization assets |

**Catalog versioning** tied to `contentVersion` in save header for migration.

### JSON

- Mods and exported layouts: schema-validated JSON (JSON Schema in `Tools/`).  
- Remote config (future): signed JSON blobs.

### Versioning & Migration

- `ISaveMigrator` chain: V1→V2→…→Current.  
- **Rule:** Never delete fields without migration; deprecate with defaults.  
- Unit tests per migrator step.

### Database Objects (future)

- Optional **SQLite** for analytics or large collection; not v1 player save.

---

## 9. Window Integration (Architecture)

### Goals

- Render **transparent URP** content in a **borderless** window.  
- Place window relative to **WorkerW / Progman** desktop layering model on Windows 11.  
- Support **click-through** with interactive islands.

### Subsystem Decomposition

```text
DesktopWindowHost
├── WindowLifecycle (create, destroy, single-instance)
├── LayeringStrategy (IWindowLayerPolicy)
│     ├── BelowDesktopIconsPolicy
│     ├── AboveWallpaperPolicy
│     └── InteractiveOverlayPolicy
├── HitTestManager (maps Unity colliders → screen regions)
├── ClickThroughController (WS_EX_TRANSPARENT, WS_EX_LAYERED)
├── DpiMonitor (per-monitor V2 awareness)
└── FocusPolicy (no activate vs interaction mode)
```

### WinAPI Surface (conceptual, no implementation)

- `HWND` ownership: Unity main window handle via plugin.  
- Extended styles: layered, transparent, toolwindow (optional, to reduce alt-tab clutter—product decision).  
- **WorkerW discovery:** documented sequence to find host behind desktop icons; fallback path if OS changes.  
- **Multi-monitor:** `EnumDisplayMonitors`, store `MonitorId` in settings.

### Unity Integration

- **Camera clear flags** alpha 0; URP 2D renderer with correct blend.  
- **Full-screen quad** only where needed; minimize overdraw.  
- Separate **UI camera** for opaque panels when not click-through.

### Risk Controls

- OS updates can break WorkerW hacks → **feature flag** to revert to “windowed overlay” mode.  
- Automated smoke test on Win11 CI VM.

### Why isolated asmdef

- Security review, minimal P/Invoke surface, mockable `IDesktopWindowHost` for editor play without Win32.

---

## 10. Save System

### Architecture

```text
SaveCoordinator
├── DirtyTracker (aggregates ISaveParticipant)
├── SnapshotBuilder (main thread: clone DTO)
├── SerializeJob (background: JSON + optional compress)
├── AtomicFileWriter (temp → replace)
├── BackupRotator (keep last N autos)
└── MigratorPipeline
```

### Autosave

- Interval: 60–120 s configurable.  
- Triggers: shop purchase, layout commit, quit.  
- Debounce rapid events.

### Manual Save

- Slot picker UI; metadata (playtime, screenshot thumb optional).

### Version Upgrade

- On load: detect version < current → migrate → validate invariants.  
- On fail: offer backup restore list.

### Backup

- `SaveBackups/` rolling files with timestamp.  
- Export zip for user.

### Compression

- Optional gzip for large gardens; trade CPU on low-end devices.

### Future Cloud Save

- `ICloudSaveAdapter` with conflict resolution policy (latest timestamp wins + merge inventory by id).  
- Offline-first always.

---

## 11. Event System

### Bus Design

- **Sync bus** for gameplay (same thread as sim).  
- **Async queue** for IO completion callbacks marshaled to main thread.

### Event Categories

| Category | Examples |
| --- | --- |
| Game | `MushroomStageChanged`, `Harvested`, `CurrencyChanged` |
| UI | `OpenShop`, `ShowTooltip`, `ModalPushed` |
| Platform | `SteamOverlayActivated`, `Suspend`, `Resume` |
| Desktop | `ClickThroughChanged`, `MonitorReconfigured` |
| Save | `SaveStarted`, `SaveCompleted`, `SaveFailed` |

### Contract Rules

- Events are **immutable records** (`readonly struct` or small classes).  
- No event carries UnityEngine.Object references across asmdefs—use ids.

### Publish / Subscribe

- Middleware: **logging**, **achievements**, **analytics** (opt-in) as subscribers.  
- Unsubscribe on dispose to prevent leaks.

### Command vs Event

- **Commands** mutate state (single handler).  
- **Events** announce facts (0..n subscribers).

---

## 12. State Machines

### Application / Game State

```text
Boot → InitializeServices → LoadContent → LoadSave → MainMenu (optional) → DesktopPlay
  ↘ ErrorRecovery ↗
DesktopPlay ↔ Paused (tray)
ShuttingDown → FlushSave → Teardown
```

### Mushroom Growth State

```text
Spore → Mycelium → Pinning → Growing → Mature → (Harvested | Decayed)
```

Transitions driven by **GrowthSystem** with guards (water, temp).

### Window State

```text
PassiveDesktop (click-through ON)
  → InteractionMode (click-through OFF, optional focus)
  → PhotoMode (freeze sim optional)
```

### Input State

```text
Default → ToolActive(Inspect|Harvest|Place) → UIBlocking
```

### UI State

```text
Stack: HUD → Panel → Modal → SystemMenu
```

**Implementation note:** Hierarchical SM with table-driven transitions in `Mushroom.Gameplay`.

---

## 13. Asset Pipeline

### Sprites & Atlas

- **Sprite Atlas** per biome + UI atlas.  
- Padding and mesh type documented for 2D lighting if used.

### Animation

- Clip naming: `{Species}_{Stage}_{Action}`.  
- Animator controllers **shared templates** with override controllers.

### Audio

- Import settings: force mono for SFX, streaming for music.  
- Addressables for large music packs.

### Localization

- Unity Localization package; string tables per feature folder.  
- Pseudo-locale for layout stress.

### Addressables Build

- CI builds catalog per platform; `contentVersion` bump policy in `Docs/ContentAuthoring`.

### Import Rules (Editor)

- Validators: power-of-two optional, max size, readable off.  
- Auto-assign labels from folder path (`Assets/_Game/Data/Species` → label `species`).

### Optimization

- Texture max 2048 for hero assets; 512 for UI icons.  
- Audio compression Vorbis/Opus per platform settings.

---

## 14. UI Architecture

### Structure

```text
UIRoot
├── HUDLayer (always on)
├── PanelLayer (inventory, guide)
├── PopupLayer (notifications)
├── ModalLayer (blocking)
└── DebugLayer (dev only)
```

### UI Manager

- **UIStackService** pushes/pops panels with focus restoration.  
- **UIViewFactory** loads UXML Addressables.

### Patterns

- **MVVM:** ViewModel per panel, binds to `IEventBus` and read-only session facades.  
- **No business logic in views.**

### Notifications & Tooltips

- Queue with priority; tooltips from `TooltipDefinition` + live data resolver.

### Transitions

- UIToolkit transitions + optional DOTween for world-linked UI (if adopted).  
- Respect `reduce motion` setting.

---

## 15. Performance Plan

### CPU Budget (per frame @ 60 FPS)

| Subsystem | Budget |
| --- | --- |
| Simulation tick (amortized) | ≤ 2 ms |
| UI layout | ≤ 1 ms |
| Gameplay scripts | ≤ 2 ms |
| Rest Unity/URP | remaining |

### GPU

- Target **< 100 draw calls** in typical scene via atlasing and static batching.  
- Limit overdraw: transparent layers only where needed.

### Pooling

- Mushroom views, particles, floating text, UI list cells.

### GC

- Zero alloc in `OnTick` hot path; object pools for commands/events if high volume.

### Memory

- Addressables release handles on biome unload.  
- Texture streaming budget conservative on iGPU.

### Update Frequency

| Mode | Sim Hz | Render Hz |
| --- | --- | --- |
| Unfocused desktop | 1–2 | 15–30 |
| Focused | 10 | 60 |
| Photo/static | 0 | on-demand |

### Idle Optimization

- **Sleep scheduler:** skip VFX updates when no visible changes.  
- **Shader LOD** and particle culling.

---

## 16. Development Roadmap

### Milestone 0 — Foundation (4–6 weeks)

| | |
| --- | --- |
| **Objectives** | Repo, asmdefs, CI compile, empty bootstrap scene |
| **Deliverables** | Composition root, event bus, logging, feature flags |
| **Dependencies** | Unity 6 LTS project template |
| **Complexity** | Medium |
| **Risk** | DI choice churn — lock interfaces early |
| **Testing** | EditMode tests for Core math |

### Milestone 1 — Desktop Shell (6–8 weeks)

| | |
| --- | --- |
| **Objectives** | Win32 transparent window, click-through, tray |
| **Deliverables** | `DesktopWindowHost`, settings, single-instance |
| **Dependencies** | M0 |
| **Complexity** | High |
| **Risk** | Win11 WorkerW breakage |
| **Testing** | Manual matrix multi-monitor; smoke automation |

### Milestone 2 — Simulation Core (6 weeks)

| | |
| --- | --- |
| **Objectives** | Time, growth, save/load v1 |
| **Deliverables** | 1 species, 3 stages, plots, autosave |
| **Dependencies** | M0 |
| **Complexity** | Medium |
| **Risk** | Save corruption — atomic writes + tests |
| **Testing** | Migrator tests, offline accrual unit tests |

### Milestone 3 — Presentation & Input (5 weeks)

| | |
| --- | --- |
| **Objectives** | Pooling, placement, harvest loop |
| **Deliverables** | Camera pan, tool modes, basic HUD |
| **Dependencies** | M1, M2 |
| **Complexity** | Medium |
| **Risk** | Hit-test vs click-through bugs |
| **Testing** | PlayMode integration |

### Milestone 4 — Content Pipeline (4 weeks)

| | |
| --- | --- |
| **Objectives** | SO authoring, Addressables, 10 species |
| **Deliverables** | Editor validators, build script |
| **Dependencies** | M2 |
| **Complexity** | Medium |
| **Risk** | Catalog drift — version pinning |
| **Testing** | Content validation CI |

### Milestone 5 — Economy & Shop (4 weeks)

| | |
| --- | --- |
| **Objectives** | Currency, shop UI, inventory |
| **Deliverables** | Rotation tables, transactions log |
| **Dependencies** | M3, M4 |
| **Complexity** | Medium |
| **Risk** | Exploit loops — telemetry hooks |
| **Testing** | Economy invariant tests |

### Milestone 6 — Weather, Seasons, Audio (5 weeks)

| | |
| --- | --- |
| **Objectives** | Ambient living world |
| **Deliverables** | Weather FSM, season modifiers, audio buses |
| **Dependencies** | M2, M3 |
| **Complexity** | Medium |
| **Risk** | Performance — quality presets |
| **Testing** | Perf baseline capture |

### Milestone 7 — Progression (4 weeks)

| | |
| --- | --- |
| **Objectives** | Achievements, guide, quests v1 |
| **Deliverables** | Event-driven unlocks, journal UI |
| **Dependencies** | M5 |
| **Complexity** | Low–Medium |
| **Risk** | Scope creep on quests |
| **Testing** | Achievement regression suite |

### Milestone 8 — Polish & Beta (8 weeks)

| | |
| --- | --- |
| **Objectives** | Photo mode, localization framework, settings completeness |
| **Deliverables** | Beta build, crash reporting, installer |
| **Dependencies** | All prior |
| **Complexity** | High |
| **Risk** | Beta feedback overload — prioritize |
| **Testing** | Full regression, soak tests |

### Milestone 9 — Commercial Release (4 weeks)

| | |
| --- | --- |
| **Objectives** | Steam integration, store page, launch |
| **Deliverables** | Gold master, day-one patch process |
| **Dependencies** | M8, legal/store assets |
| **Complexity** | Medium |
| **Risk** | Certification/desktop edge cases |
| **Testing** | Release candidate checklist |

---

## 17. Coding Standards

### Naming

- Types: `PascalCase`; private fields: `_camelCase`; constants: `PascalCase` or `kConstant`.  
- IDs: `snake_case` in data files; `SpeciesId` struct in code.

### Namespaces

- `Mushroom.Core.Growth`, `Mushroom.Gameplay.Economy`, etc.

### SOLID / DRY / KISS

- One reason to change per class; prefer small files (< 400 LOC soft cap).  
- No copy-paste curves — shared utilities.

### Clean Architecture

- Enforce with asmdef references; reject `Core → Presentation` in code review.

### Code Review Rules

- Every PR: tests for logic changes, save version impact noted, perf note if hot path.

### Documentation

- Public interfaces: XML doc mandatory.  
- Architecture decisions: `Docs/Architecture/ADR-*.md`.

### Comments & Regions

- Avoid regions in favor of partial classes only when generated.  
- Comments explain **why**, not what.

### File Organization

- One public type per file; file name matches type.

---

## 18. Testing Strategy

| Layer | Scope | Tools |
| --- | --- | --- |
| Unit | Growth math, economy, migrators, offline accrual | NUnit, EditMode |
| Integration | Save round-trip, system pipeline order | EditMode + test fixtures |
| Gameplay | Harvest loop, shop purchase | PlayMode |
| Regression | Achievement unlock matrix | CI nightly |
| Performance | Frame time, alloc tracking | Unity Profiler, custom markers |
| Platform | Win32 layering smoke | VM manual + scripted launcher |
| Manual | UX, DPI, multi-monitor | Test checklist per milestone |

**Definition of Done:** No merge without green EditMode; PlayMode for gameplay PRs.

---

## 19. Deployment Pipeline

```text
Dev branch → PR → CI (compile, tests, content validate)
  → develop build (auto)
QA branch → staging build + soak
Release branch → signed installer / Steam depot
Hotfix → cherry-pick + migrator if save bump
```

### Versioning

- SemVer `MAJOR.MINOR.PATCH`; save `MAJOR` bump only on breaking migrator.

### CI/CD

- GitHub Actions / Azure DevOps: build Windows player, run tests, publish artifacts.  
- Addressables build cached by content hash.

### Steam Build

- Depot: game binaries + redistributables; beta branches `public`, `beta`.

### Patch Policy

- Day-one patch prepared during RC; rollback via previous depot manifest.

---

## 20. Future Expansion

| Area | Direction |
| --- | --- |
| Multiplayer | Async garden visits only; no real-time sim sync in v1 design |
| Steam Workshop | Decoration/skin packs using sandboxed JSON + assets |
| AI NPCs | Schedule-based dialog, not LLM in client (cost/privacy) |
| Biomes | Addressable biome packs + new system modifiers |
| Pets | Companion entities using same component architecture as mushrooms |
| Weather | Extreme events, player-built shelters |
| Events | Time-limited tables driven by remote config |
| Cloud Sync | Adapter pattern; conflict UI |
| Mobile Companion | Read-only stats + notifications via secure API |
| Modding | Full pipeline with validator and load order manager |
| macOS/Linux | Re-evaluate desktop integration; separate host implementation |

---

## Appendix A — Key Architecture Decisions (Summary)

| Decision | Choice | Why |
| --- | --- | --- |
| Engine | Unity 6 LTS + URP 2D | Mature 2D, desktop player, team skill |
| Core logic | Pure C# asmdef | Testability |
| Content | SO + Addressables | Designer workflow, DLC |
| Save | Versioned JSON | Debuggable, mod-friendly; migrators mandatory |
| Desktop | Win32 isolated plugin | OS coupling quarantined |
| Architecture style | Systems + events + commands | Extensibility without god classes |

---

## Appendix B — Related Harness Artifacts (this repo)

- Record stack acceptance: `docs/decisions/` (next number: Unity desktop stack).  
- Break milestones into `docs/stories/` when implementation starts.  
- Update `docs/ARCHITECTURE.md` application section when game repo is linked or monorepo adopted.

---

*End of architecture baseline. Implementation requires explicit follow-up stories; no gameplay code in this document.*