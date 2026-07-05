# Balance specification — Desktop Garden (baseline)

**Trạng thái:** Draft v0.1 — số liệu **playtest sẽ chỉnh**; code đọc từ ScriptableObject tuning, không magic number rải rác.  
**Tier áp dụng:** A (VS1) bắt buộc; B/C mở rộng cột “Notes”.

---

## 1. Nguyên tắc

- **Cozy, không punish harsh:** wilt là **cảnh báo + chậm growth**, không chết cây Tier A (chết = Tier B+ optional).  
- **Offline cap** chống exploit idle vô hạn.  
- **Mưa** = gameplay relief (đỡ tưới), không auto max moisture vĩnh viễn.  
- Mọi hằng số trong `Tuning/GlobalBalance.asset` hoặc `MoistureTuning.asset`.

---

## 2. Moisture (core — Tier A)

### 2.1 Model

| Field | Type | Range | Mô tả |
| --- | --- | --- | --- |
| `moisture` | float | 0–100 | % độ ẩm ô plot |
| `decayPerSimMinute` | float | tuning | Giảm/phút sim khi không mưa |
| `rainAddPerMinute` | float | tuning | Tăng khi weather = Rain |
| `waterCanAdd` | float | tuning | Một lần tưới (click) |

### 2.2 Baseline đề xuất (VS1)

| Parameter | Value | Ghi chú |
| --- | --- | --- |
| `decayPerSimMinute` | 2.0 | 50 phút sim 100→0 nếu không mưa |
| `waterCanAdd` | 35 | ~3 lần tưới từ 0→100 |
| `rainAddPerMinute` | 8.0 | Mưa 10 phút sim ≈ +80 |
| `wiltThreshold` | 20 | Dưới → trạng thái Wilt |
| `healthyMin` | 40 | UI “comfortable” green zone |

### 2.3 Wilt effects (Tier A)

| Effect | Value |
| --- | --- |
| Growth speed multiplier | ×0.25 khi moisture < wiltThreshold |
| UI | Icon wilt trên plot; tooltip “Needs water” |
| Recovery | moisture ≥ healthyMin → bỏ wilt trong 1 tick |

### 2.4 Growth modifier từ moisture (Tier A)

```text
moistureMultiplier = lerp(0.25, 1.0, smoothstep(wiltThreshold, healthyMin, moisture))
effectiveGrowth = baseRate * speciesMod * moistureMultiplier * (weatherMod stub 1.0)
```

**Unit test:** moisture 0 → mult ≤0.25; moisture 100 → mult 1.0.

---

## 3. Growth time (Tier A — species_common_01)

| Stage | Sim minutes (baseline) | Cumulative |
| --- | --- | --- |
| Spore → Sprout | 5 | 5 |
| Sprout → Young | 15 | 20 |
| Young → Adult | 30 | 50 |
| Adult → Mature (harvest) | 45 | 95 |

**Dev time scale:** 1–100× trong `AppConfig` — không ship cho player mặc định.

**Tier B:** thêm Flower, Mutation gates theo moon (C).

---

## 4. Offline progression

| Parameter | Value |
| --- | --- |
| `maxOfflineHours` | 24 |
| `offlineSimSpeed` | 1.0× (same as online) |
| Moisture offline | Simulate decay; rain from **saved weather state** at quit + forecast stub Tier A: no rain offline unless was raining |

**Tier B:** apply last known season weather table simplified.

**Unit test:** 48h offline → chỉ accrue 24h growth/moisture delta.

---

## 5. Harvest & replant (default — O5)

| Rule | Tier A default |
| --- | --- |
| Sau harvest | Plot **empty**; cần **plant spore** (inventory) |
| Loot | 1–3 `item_harvest_common` by species table |
| Mature guard | Chỉ harvest stage ≥ Mature |

---

## 6. Economy (Tier B+ — placeholder)

| Currency | Faucet (examples) | Sink (examples) |
| --- | --- | --- |
| Coins | Sell harvest | Buy spores, decor |
| Spores | Rare harvest | Plant premium |

**VS1:** có thể **0 currency** — chỉ inventory count.

---

## 7. Weather → moisture (Tier B)

| Weather | decay mult | rain add |
| --- | --- | --- |
| Sunny | 1.2× decay | 0 |
| Cloudy | 1.0× | 0 |
| Rain | 0.5× decay | 8/min |
| Snow | 0.3× decay | 0 (moisture from snow melt Tier C) |

---

## 8. Telemetry (opt-in Tier C)

Events (không PII): `harvest`, `water`, `wilt_enter`, `session_minutes`, `crash`.  
Dùng balance iteration — không gửi save content.

---

## 9. Playtest checklist balance

- [ ] 5 phút session: player hiểu tưới ít nhất 1 lần.  
- [ ] Quên tưới 30 phút sim: thấy wilt, recovery sau tưới.  
- [ ] Mưa Tier B: không bắt tưới manual 10 phút.  
- [ ] Offline 8h: không vượt mature trong 1 session unfair.

---

*Version 0.1 — sync với `MILESTONE_DEEP_SPEC` US-M2-10/11.*