# Sprint plan — Desktop Garden (2 tuần / sprint)

**Capacity giả định:** 1 developer, **16–20h/sprint** (~8–10h/tuần). Điều chỉnh velocity sau Sprint 2.

**Legend:** ● = sprint goal | Stories = US-* / P0-*

---

## Phase map

| Sprints | Phase | Exit |
| --- | --- | --- |
| S01 | P0 close + M0 start | asmdef + bootstrap |
| S02–S03 | M0 done | tests + CI doc |
| S04–S06 | M2 sim + moisture | save v1 |
| S07–S09 | M3 VS1 | **VS1 build** |
| S10–S12 | M4 + M5 | shop loop |
| S13–S15 | M1 desktop | VS2 |
| S16–S18 | M6 + M7 | ambience + progression |
| S19–S24 | M8 beta | beta build |
| S25–S28 | M9 ship | Steam RC |
| S29–S32 | Buffer / DLC prep | post-1.0 |

---

## Sprint detail

### S01 — Project alignment

| | |
| --- | --- |
| **Goal** | Monorepo P0 done; M0 folder + asmdef started |
| **Stories** | P0-03b doc Addressables need; P0-05 `Mushrooms/Docs` symlink/copy; US-M0-01, US-M0-02 (partial) |
| **Deliverable** | `_Game` tree; asmdef compile |
| **Review** | Demo empty Bootstrap play |

### S02 — Composition root

| | |
| --- | --- |
| **Goal** | App boots with services |
| **Stories** | US-M0-03, US-M0-04, US-M0-05, US-M0-06 |
| **Deliverable** | ≥2 EditMode tests |
| **Risk** | DI scope — timebox 4h |

### S03 — Sim shell + CI

| | |
| --- | --- |
| **Goal** | M0 exit |
| **Stories** | US-M0-07, US-M0-08, US-M0-09 |
| **Deliverable** | `CI.md`; M0 epic done |
| **Proof** | T-M0-01, T-M0-02 |

### S04 — Time + species data

| | |
| --- | --- |
| **Goal** | Time ticks; SO species |
| **Stories** | US-M2-01, US-M2-02 |
| **Deliverable** | `species_common_01` asset |
| **Read** | `GAME_BALANCE_SPEC` §3 |

### S05 — Growth + session

| | |
| --- | --- |
| **Goal** | In-memory garden |
| **Stories** | US-M2-03, US-M2-04, US-M2-05 |
| **Deliverable** | T-M2-01 |

### S06 — Moisture + water + save

| | |
| --- | --- |
| **Goal** | Core USP simulation |
| **Stories** | US-M2-10, US-M2-11, US-M2-06, US-M2-07, US-M2-08, US-M2-09 |
| **Deliverable** | `SaveSchema/v1.md`; T-M2-02..06 |
| **Milestone** | M2 complete |

### S07 — Views + input

| | |
| --- | --- |
| **Goal** | See garden |
| **Stories** | US-M3-01, US-M3-02, US-M3-03 |
| **Deliverable** | DesktopPlay scene populated |

### S08 — Commands + HUD

| | |
| --- | --- |
| **Goal** | Water + harvest playable in editor |
| **Stories** | US-M3-04, US-M3-05, US-M3-11, US-M2-12 |
| **Deliverable** | T-M3-02 |

### S09 — VS1 ship

| | |
| --- | --- |
| **Goal** | **VS1 exe** |
| **Stories** | US-M3-06, US-M3-07, US-M3-08, US-M3-09, US-M3-10, US-M3-12 |
| **Deliverable** | VS1 checklist all tick |
| **Playtest** | 3 sessions ghi chú balance |

### S10 — Addressables + validators

| | |
| --- | --- |
| **Goal** | Content pipeline |
| **Stories** | P0-03b install Addressables; US-M4-01, US-M4-02, US-M4-03 |
| **Deliverable** | 5 species load async |

### S11 — Species pack + decor defs

| | |
| --- | --- |
| **Goal** | Data-only expansion |
| **Stories** | US-M4-04, US-M4-05, US-M4-06, US-M4-07 |

### S12 — Economy MVP

| | |
| --- | --- |
| **Goal** | Buy spore → plant loop |
| **Stories** | US-M5-01 … US-M5-05 |
| **Deliverable** | Shop UI v0 |

### S13–S15 — Desktop shell (M1)

Stories US-M1-01 … US-M1-11 per sprint 4–5 stories; S15 exit VS2 checklist.

### S16–S18 — M6 weather/audio + M7 progression

Split per `GAME_MASTER_PLAN` §11–12.

### S19–S24 — M8 beta

Soak test week S22; crash reporter S19.

### S25–S28 — M9 Steam

Depot, achievements, RC.

### S29–S32 — Buffer

P1 bugs, first DLC biome spec, mutation Tier C content.

---

## Ceremonies (solo)

| When | Activity |
| --- | --- |
| Sprint start | Pick stories; update backlog status |
| Mid | Balance note 15 min |
| End | Demo + update TEST_MATRIX evidence |
| Milestone | `GAME_PLAN_RESEARCH` gate review |

---

## Velocity tracking

| Sprint | Planned SP | Actual | Notes |
| --- | --- | --- | --- |
| S01 | — | | fill after |

*Story points optional; use story count if preferred.*

---

*Sprint plan v1.0 — 32 sprints to buffer.*