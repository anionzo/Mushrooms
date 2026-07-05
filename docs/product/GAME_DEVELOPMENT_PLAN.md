# Kế hoạch làm game — Tóm tắt (v1.1)

**Trạng thái:** Pre-production **~90%** — đã nghiên cứu & bổ sung; chờ **approve vision** → M0 code.

---

## Đọc theo thứ tự

1. [`GAME_PLAN_RESEARCH_AND_GAPS.md`](GAME_PLAN_RESEARCH_AND_GAPS.md) — **Đủ chưa?** Gap, Nook/Steam, art gates  
2. [`GAME_MASTER_PLAN.md`](GAME_MASTER_PLAN.md) — ~**76** story, milestone  
3. [`MILESTONE_DEEP_SPEC.md`](MILESTONE_DEEP_SPEC.md) — AC M0–M3 + moisture  
4. [`GAME_SPRINT_PLAN.md`](GAME_SPRINT_PLAN.md) — 32 sprint  
5. [`GAME_BALANCE_SPEC.md`](GAME_BALANCE_SPEC.md) — số moisture/wilt/growth  
6. [`GDD_VOL_01_EXPERIENCE.md`](GDD_VOL_01_EXPERIENCE.md) — FTUE, loops  

---

## Một trang nhớ

| Mốc | Là gì |
| --- | --- |
| **VS1** | Windows build: **tưới + độ ẩm + wilt** + harvest + save |
| **VS2** | Desktop trong suốt + click-through |
| **MVP** | Shop, weather, 80+ species path |
| **1.0** | Steam + beta |

**Thứ tự:** P0 → M0 → M2 → M3 (VS1) → M4/M5 → M1 → M6–M9  

**Repo Unity:** `Mushrooms/` (ADR 0008)

---

## Bộ tài liệu plan

| File | Vai trò |
| --- | --- |
| `DESKTOP_GARDEN_VISION.md` | Vision 25 module, tier A–D |
| `DESKTOP_IDLE_SIM_ARCHITECTURE.md` | Kiến trúc kỹ thuật |
| `CONTENT_SCHEMA_INDEX.md` | SO / save fields |
| `GDD_OUTLINE.md` | GDD 300+ trang (mục lục) |
| `docs/QA/` | VS1 + Win11 matrices |
| `docs/TEST_MATRIX.md` | Proof rows |

---

## Còn thiếu đến “GDD 500 trang studio”

Vol 2–7 GDD, wireframe từng UI, UML đầy đủ — **sau approve tier** (O2/O3 trong CONTEXT).

---

## Tiếp theo

**Approve vision** + D1–D10 → **bắt M0** (asmdef trong `Mushrooms/Assets/_Game/`).