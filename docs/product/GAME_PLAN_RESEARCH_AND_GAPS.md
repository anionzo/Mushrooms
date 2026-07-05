# Nghiên cứu & đánh giá độ đầy đủ plan — Desktop Garden

**Mục đích:** Trả lời “plan đã kỹ chưa?” — căn cứ công khai, gap so với vision 25 module, và checklist bổ sung.  
**Phiên bản:** 1.0 (sau review nội bộ tài liệu repo + landscape desktop/cozy sim)

---

## 1. Kết luận ngắn

| Khía cạnh | Trước bổ sung | Sau bổ sung (mục tiêu) |
| --- | --- | --- |
| Kiến trúc kỹ thuật | **Đủ** (`DESKTOP_IDLE_SIM_ARCHITECTURE.md`) | Giữ + link data schema |
| Vision & differentiation | **Đủ** (`DESKTOP_GARDEN_VISION.md`) | + competitive matrix |
| Master plan (story ~72) | **~75%** — thiếu moisture/water stories, FTUE, balance | `MILESTONE_DEEP_SPEC.md` + story M2/M3 mới |
| GDD | **~15%** (outline) | `GDD_VOL_01_EXPERIENCE.md` + balance spec |
| Sprint / capacity | **~40%** (lịch tuần thô) | `GAME_SPRINT_PLAN.md` 32 sprint |
| QA / TEST_MATRIX | **~5%** | Hàng planned + ma trận QA |
| Legal / Steam / privacy | **~10%** | §6 checklist |
| Art pipeline số lượng | Vision có, **thiếu** milestone giao art | §7 art gates |
| Repo thực tế | Unity `Mushrooms/` monorepo | P0 cập nhật path + packages gap |

**Verdict:** Plan **đủ để bắt M0**; **chưa đủ “studio 300 trang GDD”** cho đến khi approve tier + viết volume 2–7. Bản bổ sung này đưa plan lên **~90% cho pre-production** (solo/small team).

---

## 2. Landscape & học hỏi (không clone)

### 2.1 Desktop / wallpaper / overlay games

| Sản phẩm / nhóm | Cơ chế học được | Rủi ro nếu bắt chước |
| --- | --- | --- |
| **Mushroom Nook** ([Steam](https://store.steampowered.com/app/4211860/Mushroom_Nook/)) | Loop spawn–grow–touch–collect–decorate; scale species; Unity nhẹ | Clone UX/art → legal + không có USP |
| Wallpaper Engine / desktop pets | OS integration, performance kỳ vọng người dùng | Không phải game progression sâu |
| Idle / cozy (Stardew-like nhưng idle) | Session ngắn, offline progress | Scope farming đầy đủ quá lớn |

**Áp dụng cho Desktop Garden:**

- Giữ **cảm giác cozy + desktop presence**.  
- USP: **moisture + ecosystem + celestial/mutation** (đã có vision).  
- Performance: coi như **tier-0 feature** từ M2 (sim Hz), không để M8 mới tối ưu.

### 2.2 Mushroom Nook — feature công khai vs chúng ta

| Feature (public store / mô tả) | Nook (tham chiếu) | Desktop Garden tier |
| --- | --- | --- |
| Nhiều loài nấm | ~200 | 250+ **theo data** — ship A:5, B:30, C:120, D:250 |
| Giai đoạn growth | Có | 6–9 stages + dead/recycle |
| Tưới / chăm sóc | Có | **Moisture % + wilt** (sâu hơn) |
| Ngày/đêm | Có | + time-of-day phases + moon (C) |
| Trang trí | Có | Grid decor (C), undo session (C) |
| Tương tác chạm | Có | Command bus: water, harvest, inspect… |
| Nhẹ Windows | Có | NFR: <5% CPU idle — **test M1/M8** |
| Động vật AI | Không rõ / hạn chế | Tier C: 5–8 loài AI nhẹ |

### 2.3 Steam commercial expectations (genre cozy desktop)

- **Demo / Prologue** hoặc EA có roadmap rõ — plan: beta M8, EA optional sau MVP.  
- **Achievements** — M7 local, M9 Steam.  
- **Cloud save** — optional M9 (D9).  
- **Accessibility** cơ bản — M8 INP-04.  
- **Review bomb triggers:** performance, crash, “false wallpaper” (không click-through), save loss — **mitigate M2 save + M1 fallback**.

---

## 3. Gap analysis — 25 module vision vs plan cũ

| Module vision | Có trong master plan? | Gap | Bổ sung |
| --- | --- | --- | --- |
| 1 Desktop | M1 | OK | + QA matrix Win11 |
| 2 Camera | M3 partial | Parallax, season color | US-M6-xx / M3 follow |
| 3 Background | M4 biome | Multi-biome art gate | Art §7 |
| 4 Mushroom data | M2/M4 | Field dictionary đầy đủ | `CONTENT_SCHEMA_INDEX.md` |
| 5 Growth | M2 | Dead/recycle, legendary stage | US-M2-10 wilt |
| 6 Interaction | M3 | **Water, moisture UI** | **US-M2-11, M3-11** |
| 7 Animation | M3/M6 | Library 20+ states | Tier C content |
| 8 Particles | M6 | OK | |
| 9 Weather | M6 | Gameplay link moisture | `GAME_BALANCE_SPEC.md` |
| 10 Time | M2 | 7 phases | US-M6-01 split |
| 11–12 Animals/AI | M7/M6 | Thin stories | US-M7-08 fauna |
| 13 Decoration | M7 | OK | |
| 14–16 Inv/Eco/Shop | M5 | Multi-currency | Tier D only |
| 17 Achievement | M7 | OK | |
| 18 Save | M2 | OK | SaveSchema v1 file |
| 19–20 Audio/UI | M6/M8 | Screen list | GDD Vol 4 TOC |
| 21–22 Code/Managers | Architecture | OK | ADR 0008 |
| 23–24 Art/Anim counts | Vision only | **Production gates** | §7 |
| 25 Roadmap 15 phase | Mapped | OK | Sprint plan |

---

## 4. Gap kỹ thuật repo hiện tại

| Hạng mục | Trạng thái `Mushrooms/` | Plan action |
| --- | --- | --- |
| Unity 6 + URP 2D | Có (`manifest` URP 17.x) | P0-01 **done** |
| Input System | Có 1.19 | P0-03 partial |
| **Addressables** | **Chưa** trong manifest | **P0-03b** trước M4 |
| **Localization** | Chưa | P0-03c trước M8 |
| `Assets/_Game/` asmdef | Chưa | M0 |
| Win32 plugin | Chưa | M1 |
| Docs in Unity | Chưa link | P0-05 copy `Docs/` vào `Mushrooms/Docs` |

---

## 5. Tài liệu mới (bộ bổ sung chuẩn)

| File | Vai trò |
| --- | --- |
| `GAME_PLAN_RESEARCH_AND_GAPS.md` | **File này** |
| `GAME_BALANCE_SPEC.md` | Số liệu moisture, wilt, offline cap |
| `GAME_SPRINT_PLAN.md` | 32 sprint, goal, stories, exit |
| `MILESTONE_DEEP_SPEC.md` | AC mở rộng M0–M3 + moisture |
| `CONTENT_SCHEMA_INDEX.md` | SO/JSON field index |
| `GDD_VOL_01_EXPERIENCE.md` | FTUE, loops, personas (viết) |
| `docs/decisions/0008-*.md` | Monorepo + product name |
| `docs/QA/*.md` | Ma trận test |
| `Mushrooms/Docs/SaveSchema/v1.md` | Save v1 (khi M2) |

---

## 6. Checklist pháp lý / Steam / vận hành (pre-1.0)

| ID | Hạng mục | Milestone |
| --- | --- | --- |
| LGL-01 | EULA / Privacy policy (analytics opt-in) | M8 |
| LGL-02 | Steamworks SDK license & depot | M9 |
| LGL-03 | Asset license (font, audio, art) ledger | M4+ |
| LGL-04 | Không dùng trademark “Mushroom Nook” / clone UI | Always |
| OPS-01 | Crash reporter DPA | M8 |
| OPS-02 | Backup save policy documented | M2 |
| OPS-03 | Support email / Discord | M8 beta |

---

## 7. Art & content production gates

| Gate | Tier A (VS1) | Tier B | Tier C (MVP) |
| --- | --- | --- | --- |
| Species art | 1–5 placeholder | 30 | 80–120 |
| Growth stages/species | 4 min | 6 | 6–9 |
| Background biomes | 1 | 2 | 4 |
| Decor prefabs | 0 | 5 | 30 |
| UI screens functional | HUD | +Shop | Full §20 UI |
| Animation states/species | Idle, grow | +wind, harvest | Library §7 GDD |
| SFX | 3 placeholders | 20 | 60+ |
| Music loops | 0–1 | 2 | 4+stingers |

**Rule:** Không ship tier content trong build nếu chưa đạt gate (feature flag off).

---

## 8. Định nghĩa “plan chuẩn” — Definition of Ready (DoR) trước M0 code

- [x] Architecture baseline  
- [x] Vision + tier A–D  
- [x] Master plan + backlog index  
- [x] Research & gaps doc  
- [x] Balance spec (moisture)  
- [x] Sprint plan  
- [x] Deep spec M0–M3  
- [x] ADR monorepo  
- [x] TEST_MATRIX rows (planned)  
- [ ] User approve vision + D1–D10  
- [ ] Optional: harness `init` + story DB  

---

## 9. Thứ tự đọc sau bổ sung

1. `GAME_PLAN_RESEARCH_AND_GAPS.md` (này)  
2. `GAME_BALANCE_SPEC.md`  
3. `MILESTONE_DEEP_SPEC.md`  
4. `GAME_SPRINT_PLAN.md`  
5. `GAME_MASTER_PLAN.md` v1.1  
6. `GDD_VOL_01_EXPERIENCE.md`  

---

*Cập nhật khi có playtest competitor mới hoặc thay đổi tier ship.*