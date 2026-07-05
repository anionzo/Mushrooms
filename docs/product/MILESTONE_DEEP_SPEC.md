# Milestone deep specification — M0, M2, M3 (Tier A / VS1)

Bổ sung AC chi tiết cho `GAME_MASTER_PLAN.md`. **VS1 = moisture + water + harvest + save** trong cửa sổ Windows.

**Unity path:** `Mushrooms/` (monorepo). **Product:** Desktop Garden.

---

## VS1 definition (cập nhật — bắt buộc)

| # | Tiêu chí |
| --- | --- |
| V1 | 3 plots, moisture 0–100% hiển thị hoặc icon trạng thái |
| V2 | Tool/click **Water** tăng moisture (`GAME_BALANCE_SPEC`) |
| V3 | Wilt khi <20%; growth chậm khi wilt |
| V4 | 1 species, ≥4 stages, time sim + offline cap 24h |
| V5 | Harvest mature → inventory; plot empty; plant lại nếu có spore (optional Tier A: auto replant 1 free for FTUE) |
| V6 | Autosave + reload |
| V7 | Windows build `Builds/Win64/` |
| V8 | 10 phút idle không error |

---

## M0 — Foundation (deep)

### US-M0-01 Folder + scenes

```
Mushrooms/Assets/_Game/
  Scenes/Bootstrap.unity, DesktopPlay.unity, DevTest.unity
  Scripts/ (empty asmdef roots)
  Data/, Prefabs/, Art/Placeholders/
```

**AC:** EditorBuildSettings: Bootstrap index 0. Không gameplay code ngoài `_Game`.

### US-M0-02 Asmdef

Đồng bộ `DESKTOP_IDLE_SIM_ARCHITECTURE.md` §5 + `Mushrooms/Docs/asmdef-rules.md` (tạo file 1 trang).

### US-M0-03 Bootstrap

Services đăng ký theo thứ tự: `AppConfig` → `Log` → `EventBus` → `GameStateMachine` → `TimeService` (stub) → `SaveCoordinator` (stub).

### US-M0-04 Event bus

Minimum events: `AppReady`, `GameStateChanged`, `SimTick` (contract only).

### US-M0-08 Sim pipeline

`SimulationPipeline` ordered list; `GrowthSystem` placeholder no-op until M2.

### US-M0-09 CI

`Mushrooms/Docs/CI.md`: lệnh batchmode compile; GitHub Actions optional template.

---

## M2 — Simulation (deep + moisture)

### US-M2-01 TimeSystem

- `SimTime`: `TotalSimMinutes`, `DayIndex`, `PhaseOfDay` enum (Dawn/Morning/Noon/Afternoon/Evening/Night) — **6 pha Tier A**.  
- `OnSimTick(deltaSimMinutes)`.  
- Pause khi `GameState != Playing`.

### US-M2-02 Species + curve

`SpeciesDefinition`: `speciesId`, `displayNameKey`, `stages[]` duration minutes, `harvestLootTableId`, `moistureSensitivity` (optional mult).

### US-M2-03 GrowthSystem

Inputs: moisture mult từ `MoistureSystem` (US-M2-10). Publish `MushroomStageChanged`.

### US-M2-04 Session

```csharp
// conceptual
PlotState { PlotId, Moisture, MushroomInstance? }
MushroomInstance { EntityId, SpeciesId, Stage, StageProgress01 }
```

### US-M2-06 Save v1

Fields: `saveVersion`, `checksum`, `lastSimUtc`, `totalSimMinutes`, `plots[]`, `inventory[]`, `playerFlags`.

Doc: `Mushrooms/Docs/SaveSchema/v1.md`.

### US-M2-10 MoistureSystem (NEW)

| AC | Detail |
| --- | --- |
| M1 | Mỗi plot có moisture; decay mỗi sim tick theo balance spec |
| M2 | `GetMoistureMultiplier(plotId)` cho GrowthSystem |
| M3 | Wilt flag khi < threshold |
| M4 | EditMode: decay 50 sim min giảm đúng |
| M5 | Event `PlotMoistureChanged`, `PlotEnteredWilt` |

### US-M2-11 WaterPlotCommand (NEW)

| AC | Detail |
| --- | --- |
| W1 | `WaterPlotCommand(plotId)` + handler |
| W2 | Tăng moisture `waterCanAdd`; clamp 0–100 |
| W3 | Idempotent spam không crash; SFX hook empty OK |
| W4 | Không water khi plot null |

### US-M2-12 PlantSporeCommand (NEW — Tier A minimal)

| AC | Detail |
| --- | --- |
| P1 | Plant vào plot empty nếu có item spore |
| P2 | Spawn instance stage Spore |
| P3 | FTUE: 3 free spores in new save (tuning flag) |

---

## M3 — Presentation (deep)

### US-M3-03 Input

- Primary click plot with mushroom → select (future harvest).  
- Click plot empty / plot → **water mode** default khi cầm “watering can” (Tier A: always can).  
- Right-click optional inspect stub.

### US-M3-04 HarvestCommand

Đồng bộ O5: plot empty after harvest.

### US-M3-07 HUD

- Game day + phase of day.  
- Moisture indicator selected plot hoặc 3 icon plots.  
- Inventory count.

### US-M3-11 Moisture & water UX (NEW)

| AC | Detail |
| --- | --- |
| U1 | Visual wet/dry on plot (tint hoặc icon) |
| U2 | Click water → particle placeholder + moisture bar bump |
| U3 | Wilt visual on mushroom sprite |
| U4 | Tutorial popup lần đầu wilt (save flag `seenWiltTutorial`) |

### US-M3-12 FTUE micro-flow (NEW)

1. Start → 1 plot có spore growing.  
2. Sau 2 phút sim hoặc force stage Young → hint “Water”.  
3. Harvest hint khi Mature.  
**AC:** Flags không lặp; skip trong dev menu.

---

## Proof matrix (M0–M3)

| ID | Test | Layer |
| --- | --- | --- |
| T-M0-01 | EventBus two subscribers | EditMode |
| T-M0-02 | State Boot→Playing | EditMode |
| T-M2-01 | Growth advances | EditMode |
| T-M2-02 | Moisture decay | EditMode |
| T-M2-03 | Moisture mult wilt | EditMode |
| T-M2-04 | Water command | EditMode |
| T-M2-05 | Offline cap | EditMode |
| T-M2-06 | Save round-trip moisture+stage | EditMode |
| T-M3-01 | PlayMode harvest | PlayMode |
| T-M3-02 | PlayMode water wilt recover | PlayMode |

---

## Package prerequisites (before M4)

- `com.unity.addressables` add to manifest  
- Addressables groups doc in `M4-01`

---

*Deep spec v1.0 — aligns with GAME_MASTER_PLAN v1.1.*