# Story Backlog — Desktop Garden

**Plan v1.1:** `GAME_MASTER_PLAN.md` · **Research:** `GAME_PLAN_RESEARCH_AND_GAPS.md` · **Sprints:** `GAME_SPRINT_PLAN.md`  
**Deep AC:** `MILESTONE_DEEP_SPEC.md` · **Balance:** `GAME_BALANCE_SPEC.md` · **GDD:** `GDD_VOL_01_EXPERIENCE.md`  
**Vision:** `DESKTOP_GARDEN_VISION.md` · **CONTEXT:** `history/desktop-garden/CONTEXT.md`

**Trạng thái:** `pre-production` — plan ~90%; chờ approve vision → M0 code.

---

## Milestones

| Mốc | Epic(s) | Exit doc |
| --- | --- | --- |
| VS1 | M0, M2, M3 | `docs/QA/VS1_PLAYTEST_CHECKLIST.md` |
| VS2 | M1 | `docs/QA/DESKTOP_WIN11_MATRIX.md` |
| MVP | M4–M7 | Master plan §2 |
| 1.0 | M8–M9 | Release checklist (M9) |

---

## Epics (order)

| Epic | Stories | Status |
| --- | --- | --- |
| EPIC-P0-PREP | P0-01 done; P0-03b Addressables | in_progress |
| EPIC-M0-FOUNDATION | US-M0-01 … 09 | planned |
| EPIC-M2-SIMULATION | US-M2-01 … **12** | planned |
| EPIC-M3-VERTICAL-SLICE | US-M3-01 … **12** | planned |
| EPIC-M4-CONTENT | US-M4-01 … 07 | planned |
| EPIC-M5-ECONOMY | US-M5-01 … 07 | planned |
| EPIC-M1-DESKTOP | US-M1-01 … 11 | planned |
| EPIC-M6-AMBIENCE | US-M6-01 … 08 | planned |
| EPIC-M7-PROGRESSION | US-M7-01 … 07 | planned |
| EPIC-M8-BETA | US-M8-01 … 12 | planned |
| EPIC-M9-RELEASE | US-M9-01 … 08 | planned |

**~76 stories** total.

---

## M2 — Simulation (index)

| ID | Title |
| --- | --- |
| US-M2-01 | TimeSystem |
| US-M2-02 | SpeciesDefinition + GrowthCurve |
| US-M2-03 | GrowthSystem + FSM |
| US-M2-04 | Session model |
| US-M2-05 | SimScheduler |
| US-M2-06 | Save DTO v1 |
| US-M2-07 | SaveCoordinator |
| US-M2-08 | Offline cap |
| US-M2-09 | Save migrator v1 |
| **US-M2-10** | **MoistureSystem** |
| **US-M2-11** | **WaterPlotCommand** |
| **US-M2-12** | **PlantSporeCommand** |

## M3 — Vertical slice (index)

| ID | Title |
| --- | --- |
| US-M3-01 … US-M3-10 | (unchanged — see master plan) |
| **US-M3-11** | **Moisture & water UX** |
| **US-M3-12** | **FTUE micro-flow** |

## M0 index

US-M0-01 … US-M0-09 — see `GAME_MASTER_PLAN.md` §5.

---

## VS1 must pass

Moisture + water + wilt + harvest + save — `MILESTONE_DEEP_SPEC.md` § VS1.

---

## Decisions

ADR **0008** monorepo. D1–D10: `GAME_MASTER_PLAN.md` §20.