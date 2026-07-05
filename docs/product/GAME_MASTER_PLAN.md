# Kế hoạch phát triển game — Bản đầy đủ (đọc trước khi code)

| | |
| --- | --- |
| **Sản phẩm** | Desktop idle simulation — hệ sinh thái nấm trên Windows (không clone) |
| **Stack** | Unity 6 LTS, C#, URP 2D, JSON save, Addressables, ScriptableObjects, Win32 |
| **Repo harness** | `E:\CODE\Game\Mushrooms` (docs, stories, decisions) |
| **Repo Unity** | Tách riêng — working title `MushroomDesktop` (path bạn chốt) |
| **Kiến trúc** | `DESKTOP_IDLE_SIM_ARCHITECTURE.md` |
| **Cài Unity** | `UNITY_SETUP.md` |
| **Trạng thái plan** | Draft for review — **chưa bắt implementation** |

---

## Mục lục

1. [Tóm tắt điều hành](#1-tóm-tắt-điều-hành)  
2. [Mục tiêu & phạm vi theo giai đoạn](#2-mục-tiêu--phạm-vi-theo-giai-đoạn)  
3. [Thứ tự thực hiện & phụ thuộc](#3-thứ-tự-thực-hiện--phụ-thuộc)  
4. [Phase 0 — Chuẩn bị](#4-phase-0--chuẩn-bị)  
5. [Milestone 0 — Foundation](#5-milestone-0--foundation)  
6. [Milestone 2 — Simulation & Save](#6-milestone-2--simulation--save)  
7. [Milestone 3 — Vertical Slice (chơi được)](#7-milestone-3--vertical-slice-chơi-được)  
8. [Milestone 4 — Content Pipeline](#8-milestone-4--content-pipeline)  
9. [Milestone 5 — Economy & Shop](#9-milestone-5--economy--shop)  
10. [Milestone 1 — Desktop Shell](#10-milestone-1--desktop-shell)  
11. [Milestone 6 — Weather, Seasons, Audio](#11-milestone-6--weather-seasons-audio)  
12. [Milestone 7 — Progression](#12-milestone-7--progression)  
13. [Milestone 8 — Polish & Beta](#13-milestone-8--polish--beta)  
14. [Milestone 9 — Commercial Release](#14-milestone-9--commercial-release)  
15. [Ma trận feature → milestone](#15-ma-trận-feature--milestone)  
16. [Danh mục story đầy đủ](#16-danh-mục-story-đầy-đủ)  
17. [Lịch & ước lượng](#17-lịch--ước-lượng)  
18. [Rủi ro & giảm thiểu](#18-rủi-ro--giảm-thiểu)  
19. [Chất lượng & Definition of Done](#19-chất-lượng--definition-of-done)  
20. [Quyết định cần chốt](#20-quyết-định-cần-chốt)  
21. [Ngoài phạm vi v1 / commercial MVP](#21-ngoài-phạm-vi-v1--commercial-mvp)  
22. [Sau khi bạn đọc xong](#22-sau-khi-bạn-đọc-xong)

---

## 1. Tóm tắt điều hành

### Vision một câu

Ứng dụng desktop **nhẹ**, **luôn chạy**, mô phỏng **vườn nấm** — người chơi quan sát, thỉnh thoảng tương tác, tiến triển lâu dài qua nội dung và trang trí.

### Ba mốc sản phẩm lớn

| Mốc | Tên | Ý nghĩa với người chơi |
| --- | --- | --- |
| **VS1** | Vertical Slice v1 | Mở game Windows, thấy nấm lớn, click harvest, có save — **cửa sổ game bình thường** |
| **VS2** | Desktop Experience | Game nằm trên desktop, click xuyên qua, tray — **đúng fantasy “wallpaper game”** |
| **MVP** | Commercial MVP | Shop, nhiều loài, weather, settings, beta ổn — **bán được / Steam early** |
| **1.0** | Release | Steam, achievements, installer, RC |

### Chiến lược thứ tự (khác thứ tự “số milestone” trong architecture doc)

```text
Phase 0 → M0 → M2 → M3  ═══ VS1
              → M4 → M5     ═══ loop kinh tế đầy đủ
              → M1          ═══ VS2
              → M6 → M7     ═══ depth
              → M8 → M9     ═══ 1.0
```

**Lý do:** Win32 desktop (M1) rủi ro cao, debug khó — làm khi core loop đã chạy trong cửa sổ thường.

### Ước lượng tổng (1 dev, 15–20h/tuần)

| Giai đoạn | Tuần (ước lượng) |
| --- | --- |
| Phase 0 + M0 | 3–5 |
| M2 + M3 (VS1) | 6–9 |
| M4 + M5 | 5–7 |
| M1 (VS2) | 4–6 |
| M6 + M7 | 6–8 |
| M8 + M9 | 12–16 |
| **Tổng đến 1.0** | **~36–51 tuần** (~9–12 tháng) |

---

## 2. Mục tiêu & phạm vi theo giai đoạn

### VS1 — Vertical Slice v1 (bắt buộc trước M1)

- 1–3 plot, **≥1 species**, 3–4 growth stages.  
- Time sim + **offline progress** (có cap).  
- Harvest → **inventory** (stack đơn giản).  
- **Autosave** + load sau khi tắt app.  
- Input chuột, camera pan/zoom cơ bản.  
- HUD: thời gian in-game + số item (currency optional).  
- **Windows standalone** build, không cần transparent.

### VS2 — Desktop Experience

- DW-01–03 tối thiểu: borderless, transparent, click-through có vùng tương tác.  
- Tray + single-instance (DW-06, DW-07).  
- Settings desktop (layer, click-through mặc định).  
- Fallback mode nếu WorkerW không ổn.

### Commercial MVP (trước beta rộng)

- ≥8–10 species qua pipeline.  
- Shop + soft currency.  
- Decoration place cơ bản (DEC-01 grid).  
- Weather + season **ảnh hưởng growth** (ít nhất 2 weather, 4 season).  
- Achievements local; field guide skeleton.  
- Settings đủ SET-01–04; save SAV-01–04.

### 1.0 Release

- Steam (PLT-01), crash reporting (PLT-02).  
- Localization framework (L10N-01); ≥1 ngôn ngữ (EN) + chuẩn bị VI.  
- Photo mode (VFX-03), installer, beta feedback đã xử lý P0/P1.

---

## 3. Thứ tự thực hiện & phụ thuộc

```text
                    ┌─────────────┐
                    │  Phase 0    │
                    └──────┬──────┘
                           ▼
                    ┌─────────────┐
                    │     M0      │
                    └──────┬──────┘
                           ├──────────────────┐
                           ▼                  ▼
                    ┌─────────────┐    ┌─────────────┐
                    │     M2      │    │  M0.7 CI    │
                    └──────┬──────┘    └─────────────┘
                           ▼
                    ┌─────────────┐
                    │     M3      │─── VS1
                    └──────┬──────┘
                           ├────────────┬────────────┐
                           ▼            ▼            ▼
                    ┌─────────────┐ ┌─────────┐ ┌─────────────┐
                    │     M4      │ │   M5    │ │ M1 (sau VS1)│
                    └──────┬──────┘ └────┬────┘ └──────┬──────┘
                           └──────┬──────┘             │
                                  ▼                    ▼
                           ┌─────────────┐      VS2
                           │  M6 → M7    │
                           └──────┬──────┘
                                  ▼
                           ┌─────────────┐
                           │  M8 → M9    │
                           └─────────────┘
```

| Epic | Phụ thuộc bắt buộc | Có thể song song |
| --- | --- | --- |
| M0 | Phase 0 | — |
| M2 | M0 (asmdef, bus, bootstrap) | M0.7 CI |
| M3 | M2 | Art placeholder |
| M4 | M2 | M3 nếu đã có prefab contract |
| M5 | M3, M4 (item defs) | — |
| M1 | M3 (input/hit-test contract) | M6 sau M3 |
| M6 | M2, M3 | M7 một phần |
| M7 | M5 | — |
| M8 | M1–M7 | — |
| M9 | M8 | Marketing assets |

---

## 4. Phase 0 — Chuẩn bị

**Thời lượng:** 3–7 ngày  
**Exit:** Unity project mở được, packages đúng, git sạch, decision repo path.

| ID | Công việc | Chi tiết | Tiêu chí hoàn thành |
| --- | --- | --- | --- |
| P0-01 | Tạo Unity project | Template **2D URP**, Unity **6000.x LTS**, tên `MushroomDesktop` | Project mở không error đỏ |
| P0-02 | Git + ignore | `.gitignore` Unity chuẩn; commit initial | `git status` sạch sau commit |
| P0-03 | Packages | URP, Input System, Addressables, Test Framework, Localization (optional install) | Manifest lock |
| P0-04 | Player settings | Product name, company, default resolution, **Input System active** | Build settings có Standalone Windows |
| P0-05 | Docs link | `Docs/Architecture/` copy hoặc symlink từ harness | Đọc được architecture trong IDE |
| P0-06 | Decision record | `docs/decisions/0008-unity6-game-repository.md` | Path + license ghi rõ |
| P0-07 | Harness (optional) | `harness init` trong Mushrooms repo nếu dùng story DB | DB tồn tại |

**Không làm trong Phase 0:** gameplay scripts, Win32 plugin, Steam.

---

## 5. Milestone 0 — Foundation

**Epic:** `EPIC-M0-FOUNDATION`  
**Thời lượng:** 2–4 tuần  
**Exit:** Bootstrap scene chạy; ≥5 EditMode tests pass; asmdef graph đúng; CI compile (nếu P0-07).

### Mục tiêu

- Khung code **đúng kiến trúc** — sau này không đập lại folder.  
- **Event bus**, **logging**, **state machine**, **DI registry** sẵn sàng cho M2.

### Story chi tiết

#### US-M0-01 — Folder layout + scenes

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | P0-01 |

**Công việc:** Tạo `Assets/_Game/` theo architecture §5: `Scenes/`, `Scripts/` (theo asmdef), `Data/`, `Prefabs/`, `Art/` placeholders.

**Acceptance criteria:**

- Scenes `Bootstrap.unity`, `DesktopPlay.unity` (empty), `DevTest.unity` (optional).  
- Build settings: chỉ Bootstrap trong build list ban đầu.  
- Không script trong `Assets/` root ngoài `_Game`.

---

#### US-M0-02 — Assembly definitions

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-01 |

**Assemblies:**

| Assembly | References allowed |
| --- | --- |
| `Mushroom.Core` | None (hoặc Mathematics) |
| `Mushroom.Core.Contracts` | Core |
| `Mushroom.Gameplay` | Core, Contracts |
| `Mushroom.Infrastructure` | Core, Contracts, Gameplay (interfaces only — tránh cycle) |
| `Mushroom.Presentation` | Contracts, Gameplay (facades) |
| `Mushroom.Editor` | All (Editor only) |

**Acceptance criteria:**

- `Mushroom.Core` **không** reference `UnityEngine`.  
- Compile 0 errors.  
- Diagram dependencies trong `Docs/Architecture/asmdef.md` (tạo file ngắn).

---

#### US-M0-03 — ServiceRegistry + AppBootstrap

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-02 |

**Công việc:** `CompositionRoot`, `ServiceRegistry` (register/resolve), `AppBootstrap` MonoBehaviour trong Bootstrap scene.

**Acceptance criteria:**

- Play Bootstrap → console/log **"App ready"** sau khi register services.  
- Thứ tự: Config → Log → EventBus → StateMachine (stub).

---

#### US-M0-04 — IEventBus

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-03 |

**Acceptance criteria:**

- `Publish<T>` / `Subscribe<T>` / `Unsubscribe`.  
- EditMode: 2 subscribers nhận cùng event; unsubscribe không leak.  
- Events trong `Contracts` namespace, immutable.

---

#### US-M0-05 — ILogService

| | |
| --- | --- |
| **Lane** | tiny |
| **Phụ thuộc** | US-M0-03 |

**Acceptance criteria:**

- Categories: Sim, Save, Desktop, UI, App.  
- Levels: Debug, Info, Warn, Error.  
- Dev build: Unity `Debug.Log` adapter.

---

#### US-M0-06 — AppConfig + feature flags

| | |
| --- | --- |
| **Lane** | tiny |
| **Phụ thuộc** | US-M0-03 |

**Acceptance criteria:**

- ScriptableObject `AppConfig` trong Resources hoặc Addressables bootstrap.  
- ≥3 flags: `EnableDesktopIntegration`, `EnableEconomy`, `EnableDebugMenu`.  
- Gameplay đọc qua interface, không hardcode.

---

#### US-M0-07 — GameStateMachine (stub)

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-04 |

**States:** Boot → Initializing → Loading → Playing → Paused → ShuttingDown.

**Acceptance criteria:**

- Transition table-driven hoặc code rõ ràng.  
- EditMode: Boot → Playing không exception.  
- Invalid transition bị reject/log.

---

#### US-M0-08 — Sim pipeline stub

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-07 |

**Công việc:** `ISimulationSystem`, `SimulationPipeline` empty list, `SimScheduler` gọi tick 0 systems.

**Acceptance criteria:**

- Tick chạy ở fixed interval configurable trong Editor.  
- Profiler marker `Sim.Tick` có thể bật.

---

#### US-M0-09 — CI compile

| | |
| --- | --- |
| **Lane** | normal |
| **Phụ thuộc** | US-M0-02 |

**Acceptance criteria:**

- Script hoặc GitHub Action: `Unity -batchmode -quit -projectPath ... -executeMethod ...` **hoặc** documented manual build weekly.  
- Ghi trong `Docs/CI.md`.

---

### M0 — Rủi ro

| Rủi ro | Giảm thiểu |
| --- | --- |
| DI framework kéo dài | Chốt D2: custom registry trước; đổi VContainer sau nếu cần |
| Asmdef cycle | Review graph trong US-M0-02 |

### M0 — Proof tổng hợp

| Layer | Proof |
| --- | --- |
| Unit/EditMode | Event bus, state machine, (optional) growth math placeholder |
| Integration | Bootstrap play mode 30s không leak error |
| Platform | N/A |

---

## 6. Milestone 2 — Simulation & Save

**Epic:** `EPIC-M2-SIMULATION`  
**Thời lượng:** 3–5 tuần  
**Exit:** Không UI đẹp vẫn **fast-forward** trong Editor thấy stage đổi; save round-trip.

### Story chi tiết

#### US-M2-01 — TimeSystem

**Deliverables:** `ITimeService`, sim clock, pause, time scale, `UtcNow` cho offline.

**AC:**

- SIM-01: real-time + accelerated (scale 1–100 dev).  
- `SimTick` event mỗi tick.  
- Unit: offline `delta` tính đúng khi `lastSimUtc` cách 8h.

---

#### US-M2-02 — SpeciesDefinition + GrowthCurve

**Deliverables:** SO `SpeciesDefinition`, `GrowthCurveDefinition`, stage enum.

**AC:**

- SIM-02: ≥4 stages cho species demo `species_common_01`.  
- Data-only; không hardcode species id trong GrowthSystem.

---

#### US-M2-03 — GrowthSystem + FSM

**AC:**

- Stage advance theo curve × modifiers (modifiers = 1.0 stub).  
- EditMode: 100 tick → stage tăng.  
- Publish `MushroomStageChanged`.

---

#### US-M2-04 — Session model (plots + instances)

**AC:**

- SIM-03: 3 plots mặc định; mỗi plot 0–1 mushroom instance.  
- `EntityId` GUID stable qua save.

---

#### US-M2-05 — SimScheduler decoupled

**AC:**

- SIM tick 10 Hz default; render 60 FPS không gọi growth N lần/frame.  
- Unfocused stub: flag `Application.isFocused` giảm Hz (logic sẵn, test manual).

---

#### US-M2-06 — Save DTO v1 + schema doc

**AC:**

- SAV-04: `saveVersion = 1`.  
- JSON fields documented `Docs/SaveSchema/v1.md`.  
- Header: checksum field (CRC32 hoặc hash).

---

#### US-M2-07 — SaveCoordinator

**AC:**

- SAV-01: autosave 90s + on quit.  
- Atomic write temp→replace.  
- SAV-02 stub: 1 slot auto (3 slots ở M8).  
- Kill app giữa autosave → load backup hoặc previous file (policy documented).

---

#### US-M2-08 — Offline progression

**AC:**

- SIM-05: cap ví dụ 24h accrual; excess discarded có log.  
- Unit test cap.

---

#### US-M2-09 — ISaveMigrator chain (v1 only)

**AC:**

- Load v1 → OK; fake v0 → fail graceful + message.

---

### M2 — Proof

| Test | Mô tả |
| --- | --- |
| `Growth_Advances_WithTicks` | EditMode |
| `Offline_Accrual_Capped` | EditMode |
| `Save_RoundTrip_PreservesStage` | EditMode hoặc PlayMode |
| `Save_Atomic_OnCrash` | Manual + optional automated |

---

## 7. Milestone 3 — Vertical Slice (chơi được)

**Epic:** `EPIC-M3-VERTICAL-SLICE`  
**Thời lượng:** 3–4 tuần  
**Exit:** **VS1** — build `.exe` chơi được.

#### US-M3-01 — MushroomView + pooling

**AC:** Prefab sync stage → sprite/anim; pool ≥10 instances.

#### US-M3-02 — PlotView + scene layout

**AC:** 3 plot markers trong `DesktopPlay`; spawn views từ session.

#### US-M3-03 — Input + picking

**AC:** INP-01 mouse; raycast 2D chọn mushroom; không chọn khi miss.

#### US-M3-04 — HarvestCommand

**AC:** Mature only harvest; loot vào inventory; stage reset hoặc remove theo design (document trong CONTEXT).

#### US-M3-05 — Inventory (minimal)

**AC:** INV-01 subset: harvest item stack; event `InventoryChanged`.

#### US-M3-06 — CameraController

**AC:** Pan bounded; zoom min/max; không drift.

#### US-M3-07 — HUD minimal

**AC:** UI-01: game day/time; item count; toggle visibility hotkey.

#### US-M3-08 — Bootstrap → DesktopPlay flow

**AC:** Load save → Playing state → scene additive/single.

#### US-M3-09 — Windows dev build script

**AC:** Build ra `Builds/Win64/`; chạy máy dev không cần Editor.

#### US-M3-10 — Placeholder art pass

**AC:** 1 species readable; không final art bắt buộc.

### VS1 checklist (bạn tick khi review)

- [ ] Mở exe, thấy 3 plot và nấm lớn dần (hoặc time scale dev).  
- [ ] Click harvest, counter inventory tăng.  
- [ ] Tắt mở lại, stage/inventory giữ.  
- [ ] Không crash 10 phút idle.

---

## 8. Milestone 4 — Content Pipeline

**Epic:** `EPIC-M4-CONTENT`  
**Thời lượng:** 4 tuần  
**Exit:** Thêm species mới **không sửa code** (chỉ SO + art + addressable label).

| Story | Tóm tắt |
| --- | --- |
| US-M4-01 | Editor validator species (missing icon, stage count) |
| US-M4-02 | Addressables groups: core, species, biome |
| US-M4-03 | ContentCatalog load async + progress event |
| US-M4-04 | 8–10 species data + placeholder art |
| US-M4-05 | DecorationDefinition + 5 decor prefabs |
| US-M4-06 | Import rules doc + automated label from path |
| US-M4-07 | `contentVersion` in save header |

---

## 9. Milestone 5 — Economy & Shop

**Epic:** `EPIC-M5-ECONOMY`  
**Thời lượng:** 4 tuần  
**Exit:** Mua spore → plant → harvest → bán.

| Story | Tóm tắt |
| --- | --- |
| US-M5-01 | Wallet + transaction log (ECO-01) |
| US-M5-02 | ShopOfferTable SO + rotation by game day |
| US-M5-03 | Shop UI panel (UI-02) |
| US-M5-04 | Plant/spore consumption command |
| US-M5-05 | Sell harvest from inventory |
| US-M5-06 | Economy invariant tests (no negative currency) |
| US-M5-07 | Price tuning SO (curves) |

---

## 10. Milestone 1 — Desktop Shell

**Epic:** `EPIC-M1-DESKTOP`  
**Thời lượng:** 4–6 tuần  
**Exit:** **VS2**

| Story | Map req | Tóm tắt |
| --- | --- | --- |
| US-M1-01 | — | `Mushroom.Desktop.Win32` + `IDesktopWindowHost` mock in Editor |
| US-M1-02 | DW-01 | Transparent URP + borderless |
| US-M1-03 | DW-02 | Layering policy (3 modes) |
| US-M1-04 | DW-03 | Click-through + HitTestManager |
| US-M1-05 | DW-04 | Multi-monitor + DPI |
| US-M1-06 | DW-05 | Interaction mode toggle |
| US-M1-07 | DW-06 | System tray |
| US-M1-08 | DW-07 | Single-instance mutex |
| US-M1-09 | DW-08 | UI scale vs DPI |
| US-M1-10 | SET-03 | Settings persistence desktop section |
| US-M1-11 | — | Fallback non-Wallpaper mode |

**Testing:** Platform checklist `Docs/QA/Desktop_Win11_Matrix.md`.

---

## 11. Milestone 6 — Weather, Seasons, Audio

**Epic:** `EPIC-M6-AMBIENCE`  
**Thời lượng:** 5 tuần

| Story | Map | Tóm tắt |
| --- | --- | --- |
| US-M6-01 | WTH-02 | SeasonSystem + calendar |
| US-M6-02 | WTH-01 | Weather FSM + transitions |
| US-M6-03 | WTH-03 | Toggle real-world vs game season |
| US-M6-04 | — | Growth modifiers từ weather/season |
| US-M6-05 | VFX-01 | Pooled rain/spores (quality preset) |
| US-M6-06 | AUD-01 | Ambient layers crossfade |
| US-M6-07 | AUD-02 | SFX buses |
| US-M6-08 | SET-01 | Graphics quality presets |

---

## 12. Milestone 7 — Progression

**Epic:** `EPIC-M7-PROGRESSION`  
**Thời lượng:** 4 tuần

| Story | Map | Tóm tắt |
| --- | --- | --- |
| US-M7-01 | PRG-02 | Unlock tree data + service |
| US-M7-02 | PRG-03 | Achievements local |
| US-M7-03 | PRG-05 | Field guide UI |
| US-M7-04 | PRG-04 | 3 tutorial quests + 1 daily template |
| US-M7-05 | PRG-01 | Player mastery XP (soft) |
| US-M7-06 | DEC-01 | Decoration placement mode + grid |
| US-M7-07 | DEC-05 | Undo placement session |

---

## 13. Milestone 8 — Polish & Beta

**Epic:** `EPIC-M8-BETA`  
**Thời lượng:** 8 tuần

| Story | Tóm tắt |
| --- | --- |
| US-M8-01 | SAV-02 three manual slots + metadata |
| US-M8-02 | SAV-03 export/import zip |
| US-M8-03 | Settings full SET-01–05 |
| US-M8-04 | L10N-01 Unity Localization + EN table |
| US-M8-05 | VFX-03 Photo mode |
| US-M8-06 | INP-04 accessibility basics |
| US-M8-07 | UI notifications queue |
| US-M8-08 | PLT-02 crash reporting |
| US-M8-09 | Installer (Inno/MSIX — decision) |
| US-M8-10 | Beta branch + feedback triage process |
| US-M8-11 | OPS-01 editor fast-forward 24h |
| US-M8-12 | Performance pass vs NFR targets |

---

## 14. Milestone 9 — Commercial Release

**Epic:** `EPIC-M9-RELEASE`  
**Thời lượng:** 4 tuần (+ buffer marketing)

| Story | Tóm tắt |
| --- | --- |
| US-M9-01 | Steamworks integration PLT-01 |
| US-M9-02 | Achievements Steam sync |
| US-M9-03 | Steam depot + beta branch |
| US-M9-04 | Store page assets checklist |
| US-M9-05 | RC build + `Release_Checklist.md` |
| US-M9-06 | Day-one patch branch strategy |
| US-M9-07 | PLT-03 update channel stable/beta |
| US-M9-08 | Legal: privacy policy stub for analytics |

---

## 15. Ma trận feature → milestone

| Nhóm ID | VS1 | VS2 | MVP | 1.0 |
| --- | --- | --- | --- | --- |
| SIM-* | 01–03,05 partial | +06 | full | full |
| SAV-* | 01,04 | 01 | 01–04 | +cloud stub |
| INP-* | 01 | +02 | +03 | +04 |
| UI-* | 01 partial | 01 | 02–03 | 04–05 |
| DW-* | — | 01–08 | polish | polish |
| INV/ECO | INV minimal | — | full | +craft optional |
| WTH/VFX/AUD | — | — | core | polish |
| PRG-* | — | — | partial | full |
| PLT-* | — | — | — | 01–03 |
| L10N | — | — | framework | EN+ |
| MOD-* | — | — | — | post-1.0 |

---

## 16. Danh mục story đầy đủ

**Tổng:** 10 Phase 0 tasks + **~72 user stories** (US-Mx-xx).

| Milestone | Story IDs | Số lượng |
| --- | --- | --- |
| M0 | US-M0-01 … US-M0-09 | 9 |
| M2 | US-M2-01 … US-M2-09 | 9 |
| M3 | US-M3-01 … US-M3-10 | 10 |
| M4 | US-M4-01 … US-M4-07 | 7 |
| M5 | US-M5-01 … US-M5-07 | 7 |
| M1 | US-M1-01 … US-M1-11 | 11 |
| M6 | US-M6-01 … US-M6-08 | 8 |
| M7 | US-M7-01 … US-M7-07 | 7 |
| M8 | US-M8-01 … US-M8-12 | 12 |
| M9 | US-M9-01 … US-M9-08 | 8 |

Chi tiết AC từng story: sections 5–14 ở trên. Packet riêng từng file: tạo trong `docs/stories/` **khi bạn approve plan** (tránh trùng lặch trước khi review).

---

## 17. Lịch & ước lượng

### Gantt logic (tuần)

| Tuần | Milestone | Deliverable chính |
| --- | --- | --- |
| 1 | P0 + M0 | Project + asmdef + bootstrap |
| 2 | M0 | Bus, state, tests, CI doc |
| 3–4 | M2 | Time, growth, session |
| 5 | M2 | Save + offline |
| 6–7 | M3 | View, input, harvest |
| 8 | M3 | **VS1 build** |
| 9–10 | M4 | Pipeline + species |
| 11–12 | M5 | Shop loop |
| 13–15 | M1 | Desktop shell **VS2** |
| 16–18 | M6 | Weather/audio |
| 19–20 | M7 | Progression + decor |
| 21–28 | M8 | Beta |
| 29–32 | M9 | Steam + launch |

### Nhịp review (đề xuất)

- **Cuối mỗi milestone:** demo 15 phút + cập nhật backlog status.  
- **Sau VS1:** quyết định có đổi thứ tự M1 vs M6 không.  
- **Sau VS2:** playtest 5 người — checklist desktop.

---

## 18. Rủi ro & giảm thiểu

| ID | Rủi ro | P | I | Mitigation |
| --- | --- | --- | --- | --- |
| R1 | Win11 WorkerW thay đổi | M | H | Fallback windowed overlay; feature flag |
| R2 | Save corruption | M | H | Atomic write, backups, tests M2 |
| R3 | Scope creep quests/MMO | H | M | VS1/VS2 locked; M7 quest cap = 3+1 daily |
| R4 | Performance desktop idle | M | H | Sim/render split từ M2; profiling M8 |
| R5 | Solo burnout | M | H | Milestone nhỏ; VS1 sớm để motivation |
| R6 | Addressables complexity | M | M | M4 dedicated; core local trước |
| R7 | Steam delay legal/tax | L | M | M9 buffer; wishlist sớm |

---

## 19. Chất lượng & Definition of Done

### DoD cho mọi story

- AC trong section tương ứng **đều pass**.  
- Không warning mới Unity (hoặc listed known).  
- EditMode/PlayMode test cập nhật nếu logic domain đổi.  
- Không merge gameplay code vi phạm asmdef.

### DoD milestone

- Demo script trong `Docs/Demos/Mx.md`.  
- Backlog epic → `done`.  
- NFR spot-check nếu milestone chạm perf/desktop/save.

### TEST_MATRIX (harness) — hàng sẽ thêm khi implement

| Behavior | Unit | Integration | E2E | Platform |
| --- | --- | --- | --- | --- |
| Growth stage advance | ✓ | ✓ | | |
| Save round-trip | ✓ | ✓ | ✓ | |
| Harvest loop | | ✓ | ✓ | |
| Desktop click-through | | | ✓ | ✓ Win11 |
| Shop purchase | ✓ | ✓ | ✓ | |

---

## 20. Quyết định cần chốt

Bạn điền **Chọn** khi đọc xong — agent ghi vào `history/desktop-mushroom/CONTEXT.md` + `docs/decisions/`.

| ID | Câu hỏi | Tùy chọn | Gợi ý | Chọn (bạn) |
| --- | --- | --- | --- | --- |
| D1 | UI stack | UIToolkit only / uGUI only / hybrid | Hybrid | |
| D2 | DI | Custom registry / VContainer / Zenject | Custom hoặc VContainer | |
| D3 | Unity repo path | `E:\CODE\Game\???` | | |
| D4 | Tên game | | working: MushroomDesktop | |
| D5 | Sau harvest | Respawn spore / plot empty cần plant lại | Plant lại (gắn M5) | |
| D6 | Monetization | Premium / F2P+cosmetic / DLC only | Premium + DLC biomes | |
| D7 | Ngôn ngữ 1.0 | EN only / EN+VI | EN ship, VI fast-follow | |
| D8 | Installer | Inno Setup / MSIX / zip only beta | Inno beta | |
| D9 | Cloud save 1.0 | Có Steam cloud / không | Steam optional | |
| D10 | M1 vs M6 sau VS1 | Desktop trước / Weather trước | Desktop nếu USP là wallpaper | |

---

## 21. Ngoài phạm vi v1 / commercial MVP

Cố ý **không** làm đến khi post-1.0 (trừ architecture hook):

- Multiplayer real-time  
- LLM NPC in-client  
- Mobile companion app  
- MOD-01–03 full (chỉ folder StreamingAssets stub)  
- F2P aggressive monetization  
- macOS/Linux desktop host  
- Anti-cheat beyond save checksum  
- Crafting ECO-03 (optional — nếu thiếu thời gian bỏ)  
- 3 manual save slots → có thể trượt từ M8 nếu cần ship sớm (vẫn có autosave)

---

## 22. Sau khi bạn đọc xong

1. **Comment / chỉnh** trong chat: thứ tự, scope VS1, quyết định D1–D10.  
2. Khi ok: ghi `CONTEXT.md` + tạo story packets `docs/stories/US-M0-01.md` …  
3. Bắt code chỉ khi bạn nói **“approve plan”** hoặc **“bắt M0”** + path Unity.

**File liên quan:**

| File | Vai trò |
| --- | --- |
| `GAME_MASTER_PLAN.md` | **Bản này** — đọc đầy đủ |
| `GAME_DEVELOPMENT_PLAN.md` | Tóm tắt ngắn + link master |
| `DESKTOP_IDLE_SIM_ARCHITECTURE.md` | Kiến trúc kỹ thuật sâu |
| `docs/stories/backlog.md` | Trạng thái epic/story |

---

*Phiên bản plan: 1.0 — draft for author review.*