# GDD Volume 1 — Player Experience (Desktop Garden)

**Version:** 0.1  
**Pages equivalent:** ~35–45  
**Depends on:** `DESKTOP_GARDEN_VISION.md`, `GAME_BALANCE_SPEC.md`

---

## 1. High concept

The player's **Windows desktop** becomes a **living garden layer**: mushrooms grow in soil plots with **real moisture needs**, react to **time of day**, and later to **weather and seasons**. Interaction is **optional and short**; the world **continues simulating** at low cost when the player works elsewhere.

**Emotional target:** calm competence — “I keep this little world healthy.”

**Not target:** stress farming, FOMO timers, PvP, narrative epic.

---

## 2. Design pillars (playable)

| Pillar | Player feels | Failure if |
| --- | --- | --- |
| Water matters | Tưới đúng lúc = thưởng rõ | Moisture chỉ cosmetic |
| Desktop respect | Không làm máy nóng / lag | >10% CPU idle |
| Discovery | Hiếm: đêm, trăng, mutation | Paywall species |
| Expression | Decor layout | Chỉ grid shop UI |
| Fair idle | Offline có cap | 7 ngày offline = max everything |

---

## 3. Personas

### P1 — Ambient worker (primary)

- **Context:** Code/write với game windowed hoặc desktop mode.  
- **Session:** 0–2 min mỗi 30–60 phút real.  
- **Needs:** Glance moisture/wilt; one-click water; no modal spam.

### P2 — Collector

- **Session:** 15 min buổi tối.  
- **Needs:** Bestiary, rarity, mutation log, photo.

### P3 — Decorator

- **Session:** 20 min cuối tuần.  
- **Needs:** Grid place, undo, themes theo season.

---

## 4. Core loops

### 4.1 Micro loop (30s–2min)

```text
Glance plot → See wilt/moisture low → Click water →
See feedback (wet VFX, bar) → Return to work
```

### 4.2 Session loop (5–15min)

```text
Water all plots → Harvest mature →
Check inventory → Buy spore/decor (Tier B+) →
Optional rearrange decor
```

### 4.3 Meta loop (days–weeks)

```text
Complete bestiary % → Unlock biome/decor tier →
Season change → New shop rotation →
Rare event (moon, eclipse) → Mutation hunt
```

---

## 5. First-time user experience (FTUE)

### 5.1 Principles

- Teach **moisture before economy**.  
- **No** text wall; 3 guided moments max Tier A.  
- Skippable after first save.

### 5.2 Beat sheet (Tier A build)

| Step | Trigger | UI | Success |
| --- | --- | --- | --- |
| 1 Welcome | First Boot | “Your garden lives on your desktop.” | Click continue |
| 2 Watch grow | Auto | Point to one growing mushroom | Wait or time skip dev |
| 3 Water | Moisture <40% or timer 2 sim min | Highlight plot + can icon | Water once |
| 4 Wilt (soft) | Optional force wilt in tutorial save | “Plants slow when dry” | Water recover |
| 5 Harvest | Mature | Highlight mushroom | +1 inventory |
| 6 Save | After harvest | “Autosaved” toast | — |

**Flags:** `ftue_step`, `seenWiltTutorial` in save.

### 5.3 Desktop mode FTUE (Tier B — VS2)

Separate 2-step: “Interaction mode” toggle; click-through vs click garden.

---

## 6. Progression & pacing

| Phase | Real days (casual) | Content |
| --- | --- | --- |
| Hour 1 | Day 1 | 1 species, 3 plots, water/harvest |
| Day 2–3 | | 2–3 species, shop (Tier B) |
| Week 1 | | 10+ species, weather |
| Month 1 | | Decor, achievements, moon (C) |

**No** energy stamina system.

---

## 7. Difficulty & accessibility

- **Wilt:** slowdown, not instant death (Tier A).  
- **UI scale:** 100–150% (M8).  
- **Reduce motion:** fewer particles, no screen shake.  
- **Color:** wilt uses icon + pattern, not red-only.

---

## 8. UX principles (screens)

| Screen | Default state | Desktop mode |
| --- | --- | --- |
| HUD | Minimal bars | Fade when click-through |
| Shop | Closed | Hotkey / tray |
| Settings | Modal | Same |
| Photo | Full hide HUD | Pause sim optional |

Full wireframes → `GDD_OUTLINE` Part VI (Vol 4).

---

## 9. Audio experience (player-facing)

| Time phase | Player hears |
| --- | --- |
| Morning | Light birds (low vol) |
| Night | Crickets, subtle |
| Rain | Rain on leaves — ducks music 20% |

**Mixer:** SFX > ambient > music for desktop etiquette.

---

## 10. Monetization (player trust)

**Recommended:** Premium base game + cosmetic / biome DLC.  
**Avoid:** Pay-to-grow, loot box spores, F2P timer.

---

## 11. Social & UGC (future)

- Steam screenshots / photo mode.  
- Workshop decor (post-1.0).  
- No PvP.

---

## 12. Open questions (track in CONTEXT)

- Auto-replant vs manual after harvest (default manual + 3 FTUE spores).  
- Severity of wilt Tier B (death vs dormant).  
- EA vs full release pricing.

---

*Vol 1 complete for review — next Vol 2 Systems Deep or Vol 3 Content Schema on approve.*