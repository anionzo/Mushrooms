# Story Backlog — Desktop Mushroom Ecosystem

**Vision:** `docs/product/DESKTOP_GARDEN_VISION.md` · **GDD:** `GDD_OUTLINE.md` · **CONTEXT:** `history/desktop-garden/CONTEXT.md`  
**Plan:** `GAME_MASTER_PLAN.md` · **Architecture:** `DESKTOP_IDLE_SIM_ARCHITECTURE.md`

**Trạng thái tổng:** `vision-review` — chờ approve vision + tier; sau đó bổ sung story moisture/water (Tier A).

---

## Product milestones (không trùng số M trong architecture)

| Mốc | Epic(s) | Ý nghĩa |
| --- | --- | --- |
| VS1 | M0, M2, M3 | Chơi được, windowed |
| VS2 | M1 | Desktop wallpaper mode |
| MVP | M4, M5, M6, M7 | Depth + economy |
| 1.0 | M8, M9 | Beta + Steam |

---

## Epics (thứ tự thực hiện)

| Epic | Milestone | Stories | Status |
| --- | --- | --- | --- |
| EPIC-P0-PREP | Phase 0 | P0-01 … P0-07 (tasks) | planned |
| EPIC-M0-FOUNDATION | M0 | US-M0-01 … 09 | planned |
| EPIC-M2-SIMULATION | M2 | US-M2-01 … 09 | planned |
| EPIC-M3-VERTICAL-SLICE | M3 | US-M3-01 … 10 | planned |
| EPIC-M4-CONTENT | M4 | US-M4-01 … 07 | planned |
| EPIC-M5-ECONOMY | M5 | US-M5-01 … 07 | planned |
| EPIC-M1-DESKTOP | M1 | US-M1-01 … 11 | planned (sau VS1) |
| EPIC-M6-AMBIENCE | M6 | US-M6-01 … 08 | planned |
| EPIC-M7-PROGRESSION | M7 | US-M7-01 … 07 | planned |
| EPIC-M8-BETA | M8 | US-M8-01 … 12 | planned |
| EPIC-M9-RELEASE | M9 | US-M9-01 … 08 | planned |

**Tổng user stories:** ~72 (AC trong master plan §5–14).

---

## Story index — M0 (Foundation)

| ID | Title | Lane |
| --- | --- | --- |
| US-M0-01 | Folder layout + Bootstrap/DesktopPlay scenes | normal |
| US-M0-02 | Assembly definitions graph | normal |
| US-M0-03 | ServiceRegistry + AppBootstrap | normal |
| US-M0-04 | IEventBus + tests | normal |
| US-M0-05 | ILogService | tiny |
| US-M0-06 | AppConfig feature flags | tiny |
| US-M0-07 | GameStateMachine stub | normal |
| US-M0-08 | Simulation pipeline + scheduler stub | normal |
| US-M0-09 | CI / batch compile | normal |

## Story index — M2 (Simulation)

| ID | Title |
| --- | --- |
| US-M2-01 | TimeSystem |
| US-M2-02 | SpeciesDefinition + GrowthCurve SO |
| US-M2-03 | GrowthSystem + FSM |
| US-M2-04 | Session model plots + instances |
| US-M2-05 | SimScheduler decoupled from render |
| US-M2-06 | Save DTO v1 + schema doc |
| US-M2-07 | SaveCoordinator atomic autosave |
| US-M2-08 | Offline progression + cap |
| US-M2-09 | Save migrator v1 only |

## Story index — M3 (Vertical Slice → VS1)

| ID | Title |
| --- | --- |
| US-M3-01 | MushroomView + pooling |
| US-M3-02 | PlotView scene layout |
| US-M3-03 | Input picking 2D |
| US-M3-04 | HarvestCommand |
| US-M3-05 | Inventory minimal |
| US-M3-06 | CameraController |
| US-M3-07 | HUD minimal |
| US-M3-08 | Bootstrap → DesktopPlay flow |
| US-M3-09 | Windows build script |
| US-M3-10 | Placeholder art pass |

## Story index — M4 / M5 / M1 / M6 / M7 / M8 / M9

Xem bảng đầy đủ trong `GAME_MASTER_PLAN.md` §8–14 và §16.

---

## Vertical Slice v1 exit (checklist)

- [ ] Exe: plots + mushroom growth visible  
- [ ] Harvest → inventory  
- [ ] Restart → state restored  
- [ ] 10 phút idle không crash  

Chi tiết: master plan §7.

---

## Decisions pending (block nothing until M0 code)

D1–D10 trong master plan §20 — điền khi review.