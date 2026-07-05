# CONTEXT — Desktop Garden (locked / open decisions)

**Feature slug:** `desktop-garden`  
**Status:** vision draft — not locked for execution  
**Sources:** user vision (modules 1–25, world sim, 250+ mushrooms), `DESKTOP_GARDEN_VISION.md`, `GDD_OUTLINE.md`

---

## Locked (proposed — confirm with "approve vision")

| ID | Decision | Rationale |
| --- | --- | --- |
| L1 | **Không clone** Mushroom Nook; học loop công khai Steam | Legal/identity |
| L2 | **USP:** desktop **ecosystem** (nấm + moisture + weather + celestial), không chỉ collection nấm | Differentiation |
| L3 | **Implementation:** Services/Systems + asmdef; **không** god Manager list | Architecture doc |
| L4 | **Ship theo tier** A→D; 250+ species = Tier D target, không VS1 | Scope control |
| L5 | **Moisture + watering** = core gameplay Tier A | Design pillar |
| L6 | **Unity 6 LTS, URP 2D, JSON save, Win32 desktop** | Stack decision pending ADR |

---

## Open (need user input)

| ID | Question | Options |
| --- | --- | --- |
| O1 | Product name ship | Desktop Garden / other |
| O2 | Steam ship tier | B early access vs C MVP |
| O3 | Species at 1.0 | 80 / 120 / 250+ phased |
| O4 | Animals at launch | 0 / 3 / 8 |
| O5 | Moon + mutation at launch | Tier B minimal vs Tier C full |
| O6 | Monetization | Premium + DLC biome / cosmetic only (recommended) |
| O7 | Unity project path | TBD |
| O8 | GDD next volume | Vol 1 Experience vs Vol 3 Content schema |
| O9 | After VS1 priority | M1 desktop vs M6 weather depth |

---

## Out of scope until post-MVP (default)

- Multiplayer  
- LLM NPCs  
- macOS/Linux desktop host  
- Full mod marketplace  
- 22 singleton Managers as coded pattern  

---

## Next harness actions (when user approves)

1. Update `GAME_MASTER_PLAN.md` product name + Tier A moisture/water stories.  
2. Add ADR `0008-unity6-desktop-garden.md`.  
3. Slice stories US-M2-xx for `MoistureSystem`, `WaterPlotCommand`.  
4. Begin `GDD_VOL_01_EXPERIENCE.md` if O8 = Vol 1.