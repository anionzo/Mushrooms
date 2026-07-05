# Desktop Garden — Product Vision (không clone Mushroom Nook)

**Working title:** Desktop Garden  
**Thể loại:** Desktop idle / living ecosystem simulation  
**Nền tảng:** Windows 11, Unity 6 LTS, URP 2D  
**Trạng thái:** Vision draft — chờ bạn duyệt trước khi mở rộng GDD đầy đủ  

**Tham chiếu đối thủ (công khai):** [Mushroom Nook trên Steam](https://store.steampowered.com/app/4211860/Mushroom_Nook/) — spawn/grow/interact/collect/decorate, ~200 nấm, ngày/đêm, trang trí, nhẹ; Unity. Chúng ta **học vòng lặp**, không sao chép nội dung hay UX 1:1.

---

## 1. Một câu pitch

**Desktop của bạn là một khu vườn sống** — nấm, cây, thời tiết, động vật nhỏ và chu kỳ mặt trời/mặt trăng chạy nền; bạn **tưới, thu hoạch, trang trí** khi muốn, thế giới vẫn tiếp tục khi không chạm.

---

## 2. Khác biệt có chủ đích (so với “chỉ nấm” / Nook-like)

| Trục | Mushroom Nook (tham chiếu công khai) | Desktop Garden (đề xuất) |
| --- | --- | --- |
| Chủ thể | Chủ yếu nấm | **Hệ sinh thái**: nấm + đất + độ ẩm + thời tiết + động vật + nền biome |
| Chăm sóc | Tưới, tương tác | **Độ ẩm từng ô**, nhiều loại nước, wilt & recovery |
| Thời gian | Ngày/đêm | **Time-of-day 7+ pha** + **mùa** + **pha trăng 8** ảnh hưởng spawn/mutation |
| Thời tiết | Có ambience | **Weather gameplay**: mưa = không tưới; storm/snow/event đặc biệt |
| Tiến hóa | Nhiều loài nấm | **250+** phân tier (common → event) + **mutation có điều kiện** (moon + rain + …) |
| Sinh vật | (hạn chế / ambience) | **AI nhẹ** (butterfly, snail, firefly đêm…) — state machine, không MMO |
| Desktop | Wallpaper-style | **Module Desktop** đầu tiên-class: WorkerW, click-through, multi-DPI |
| Kinh tế | Shop/collect | **Đa tiền tệ có kiểm soát** (coins, spores, crystal…) + rotation shop theo season/event |
| Sự kiện hiếm | (nếu có) | **Eclipse, blood moon, meteor, aurora, cherry rain** — lịch + RNG có cap |

**Nguyên tắc:** Cạnh tranh bằng **chiều sâu simulation + identity**, không bằng “200 nấm giống y hệt”.

---

## 3. Fantasy người chơi (core loop mở rộng)

```text
Quan sát desktop (ambient)
    → Tưới / điều chỉnh độ ẩm (gameplay chính)
    → Thu hoạch / thu spores đặc biệt (đêm, trăng, event)
    → Mua hạt / decor / tool (shop theo ngày/mùa/event)
    → Trang trí & bố cục (expression)
    → Collection / bestiary / achievement
    → Quay lại (offline progress có cap, công bằng)
```

**Vòng Spawn → Grow → Interact → Collect → Decorate → Ambience** (giống nhóm hành vi Nook) được **giữ** nhưng **Grow** và **Interact** gắn **moisture, weather, moon, temperature**.

---

## 4. World Simulation (lớp nền luôn chạy)

```text
Desktop (render + input)
├── TimeSystem          (time-of-day, season, calendar)
├── CelestialSystem     (sun path, moon phase, rare sky events)
├── WeatherSystem       (FSM + blend + gameplay flags)
├── EnvironmentModel    (temperature, humidity per cell / plot)
├── EcosystemDirector   (spawn tables, animal schedules)
└── AmbienceDirector    (audio layers, particles, color grading)
```

Mọi hệ thống trên **tick thấp khi unfocused** (architecture NFR đã có).

---

## 5. Phạm vi theo tier (tránh “80 systems day 1”)

Bạn liệt kê ~25 module — đúng hướng **commercial**, nhưng cần **tier** để ship được.

### Tier A — Vertical Slice v1 (bắt buộc trước desktop trong suốt)

- Time: 1 chu kỳ ngày/đêm đơn giản (4–6 pha), chưa trăng đủ 8 pha  
- 1 biome background, 1–3 plot, **moisture + water can**  
- 1–5 species nấm, growth 4–6 stage  
- Harvest → inventory → autosave  
- Cửa sổ Windows thường  

### Tier B — Desktop Experience + depth

- Desktop module (transparent, click-through, tray)  
- Weather 4–5 loại gameplay (sunny, rain, snow, fog, windy)  
- Mùa 4, modifier growth  
- Shop daily + soft currency  
- 20–30 species qua pipeline  

### Tier C — Steam MVP (cạnh tranh)

- Moon phases + 1–2 mutation chain  
- Animals 5–8 với AI state machine  
- 80–120 species + decor pipeline  
- Achievements, bestiary, settings đầy đủ  
- Photo mode, beta, crash report  

### Tier D — “Studio scale” (6–12+ tháng sau MVP)

- 250+ species, event shop, đa tiền tệ đầy đủ  
- Sky events (eclipse, meteor shower, aurora…)  
- 10+ animals, nhiều biome background  
- Cloud save, Steam achievements, localization  
- Art targets: hundreds sprites / animations (theo capacity team)  

**Số liệu “80 systems / 100k LOC”** = **đích Tier D**, không phải điều kiện VS1.

---

## 6. Module map (25 module của bạn → kiến trúc)

| # | Module bạn | Bounded context / systems (architecture) |
| --- | --- | --- |
| 1 | Desktop | `DesktopWindowHost`, `HitTest`, `Monitor/DPI` — **không** `DesktopManager` monolith |
| 2 | Camera | `CameraController`, `ParallaxLayers`, `SeasonColorGrading` |
| 3 | Background | `BiomeDefinition`, Addressables `biome_*` |
| 4 | Mushroom | `SpeciesDefinition`, `MushroomInstance`, components |
| 5 | Growth | `GrowthSystem` + stage FSM + recycle/dead |
| 6 | Interaction | Commands: Water, Harvest, Pet, Move, Sell… |
| 7 | Animation | `AnimationDirector` + per-entity override controllers |
| 8 | Particles | `ParticlePoolService`, weather-linked emitters |
| 9 | Weather | `WeatherSystem` |
| 10 | Time | `TimeSystem` + `TimeOfDayPhase` |
| 11 | Animals | `FaunaSystem` + per-species AI graph |
| 12 | AI | Shared `AiStateMachine` library |
| 13 | Decoration | `DecorationSystem` + occupancy grid |
| 14 | Inventory | `InventorySystem` |
| 15 | Economy | `EconomySystem` + wallets |
| 16 | Shop | `ShopSystem` + rotation tables |
| 17 | Achievement | `AchievementSystem` |
| 18 | Save | `SaveCoordinator` + migrators |
| 19 | Audio | `AudioDirector` + buses |
| 20 | UI | `UIStackService` + panels (inventory, bestiary, …) |
| 21–22 | Code / Managers | **Thay bằng** Services + Systems + DI — xem §7 |
| 23–24 | Art / Animation lib | Content authoring + Addressables labels |
| 25 | Roadmap 15 phase | Map vào `GAME_MASTER_PLAN.md` + `GDD_OUTLINE.md` §Roadmap |

---

## 7. Cảnh báo kiến trúc: 22 “Manager”

Danh sách `GameManager`, `SaveManager`, `WeatherManager`… là **mô tả chức năng hợp lệ**, nhưng **implementation** phải theo `DESKTOP_IDLE_SIM_ARCHITECTURE.md`:

| Tránh | Dùng |
| --- | --- |
| `XxxManager` static singleton ôm mọi thứ | `IXxxService` / `XxxSystem` + `SimulationPipeline` |
| God `GameManager` | `GameStateMachine` + coordinators mỏng |
| Logic trong UI | Commands + event bus |

**Mapping nhanh:**

```text
TimeManager        → TimeSystem + ITimeService
GrowthManager      → GrowthSystem
SpawnManager       → SpawnSystem + EcosystemDirector
WeatherManager     → WeatherSystem
EconomyManager     → EconomySystem
UIManager          → UIStackService + presenters
SaveManager        → SaveCoordinator
```

---

## 8. Nấm & nội dung (design targets Tier C–D)

### Phân tier (đề xuất số lượng)

| Tier | Số lượng | Ghi chú |
| --- | --- | --- |
| Common / Rare / Epic / Legendary / Mythic / Secret | 150 base | Data-driven |
| Seasonal | 50 | Gắn `Season` |
| Event | 50 | Gắn `LiveOpsEvent` |
| **Tổng** | **250+** | Ship dần theo season pack |

### Thuộc tính entity (ScriptableObject + runtime)

`Id`, `Family`, `Biome`, `Rarity`, `HumidityRange`, `TempRange`, `PreferredTime`, `PreferredSeason`, `GrowthCurve`, `MutationTable`, `Glow`, `SfxId`, `ParticleId`, `SpecialAbilityId`, `Drops`.

### Growth stages (design)

`Seed → Sprout → Small → Teen → Adult → Flower → [Mutation/Ancient] → Dead → Recycle`

### Mutation (ví dụ design, không code)

- Blue + moonlight + rain → Moon Bloom  
- Golden + rainbow weather → Rainbow variant  
- Điều kiện là **data** (`MutationRecipe`), không hardcode trong C#.

---

## 9. Gameplay chính: nước & độ ẩm

- Mỗi plot/cell: **Moisture 0–100%**, decay theo thời gian & weather.  
- `< 20%` → **Wilt** (penalty growth hoặc stage regress — chốt trong GDD balance).  
- Mưa → moisture tăng, **skip manual water** (UX thông báo nhẹ).  
- Loại nước (Tier C+): Normal, Rain, Magic, Moon, Golden — item/consumable.

---

## 10. Celestial & sky (Tier C+)

- Sun: arc, golden hour, color grading keys.  
- Moon: 8 phases → modifier spawn/mutation.  
- Sky: stars, shooting stars, aurora, fireflies (night).  
- Rare: eclipse, blood moon, meteor shower, cherry blossom wind — **EventScheduler** + table.

---

## 11. Động vật & AI (Tier C)

- Species list theo phase (day/night): butterfly day, firefly/owl night.  
- AI chung: Idle → Walk → Search → Eat → Sleep → Flee (đơn giản, 2D wander).  
- Không pathfinding AAA — **đủ believable** trên desktop nhẹ.

---

## 12. Kinh tế & shop (Tier B–C)

- Wallets: Coins (core), Spores, Crystal, Star, Diamond, Event Token — **bật dần** theo tier, tránh inflation sớm.  
- Shop tabs: Daily, Weekly, Season, Event, Legendary — rotation data-driven.

---

## 13. UI surfaces (Tier B–C)

Inventory, Collection, **Bestiary**, Shop, Map/Biome, Quest, Achievement, Photo, Settings, Save slots, Language — khớp module 20; wireframe chi tiết trong **GDD Outline** (chưa vẽ 300 trang trong repo lần này).

---

## 14. Art & animation (ước lượng đích Tier D)

| Loại | Đích (team art) | Ghi chú |
| --- | --- | --- |
| Mushroom sprites | 250+ definitions, ít hơn unique mesh nếu palette swap | Atlas theo biome |
| Decoration | 200 | |
| UI | 150 | UIToolkit + icons |
| Background | 100 layers / variants | Parallax |
| Animals | 80 | |
| Particles | 200 presets | Pooled |
| Animations | 150+ libraries | Shared templates |

Prototype dùng **placeholder** đến hết Tier B.

---

## 15. Roadmap 15 phase (của bạn) ↔ plan harness

| Phase bạn | Nội dung | Map milestone |
| --- | --- | --- |
| 1–2 | Desktop Engine + Window API | M0 + M1 |
| 3 | Renderer | M0 URP + M3 presentation |
| 4 | World | M2 + M3 scene |
| 5–6 | Spawn + Growth | M2 + M4 |
| 7–8 | Animation + Interaction | M3 + M7 |
| 9 | Decoration | M7 |
| 10 | Inventory | M3 minimal → M5 |
| 11 | Weather | M6 |
| 12 | Audio | M6 |
| 13 | UI | M3 HUD → M5/M7/M8 |
| 14 | Optimization | M8 |
| 15 | Steam | M9 |

**Thứ tự implementation vẫn ưu tiên:** sim + slice windowed **trước** desktop API đầy đủ (xem `GAME_MASTER_PLAN.md`).

---

## 16. GDD đầy đủ 300–500 trang — cách làm trong repo

Không dump 500 trang một lần. Cấu trúc:

1. **`GDD_OUTLINE.md`** — mục lục + metadata (đã tạo).  
2. Từng **volume** (~30–50 trang logic): Systems, Content, UI, Art bible, Live ops.  
3. Story harness `docs/stories/` bám **tier** A→D.

Bạn approve vision này → volume tiếp theo: **UI wireframe spec** + **content schema** + **sprint breakdown**.

---

## 17. Quyết định cần bạn chốt (vision)

| ID | Câu hỏi | Gợi ý |
| --- | --- | --- |
| V1 | Tên ship | Desktop Garden |
| V2 | USP một dòng marketing | “Living desktop ecosystem — water, weather, moon, mutations” |
| V3 | Tier ship Steam | C (MVP) hay B (early access sớm) |
| V4 | Nấm launch | 30 vs 80 vs 120 |
| V5 | Animals launch | 0 vs 3 vs 8 |
| V6 | Mutation launch | Tier C only vs vài cái Tier B |
| V7 | Monetization | Premium + DLC biome / cosmetic (tránh pay-to-grow) |

---

## 18. Liên kết tài liệu

| File | Vai trò |
| --- | --- |
| `DESKTOP_GARDEN_VISION.md` | **File này** — vision & differentiation |
| `GDD_OUTLINE.md` | Mục lục GDD + section đã điền |
| `DESKTOP_IDLE_SIM_ARCHITECTURE.md` | Kỹ thuật |
| `GAME_MASTER_PLAN.md` | Milestone & story ~72 |

---

*Chờ bạn: “approve vision” / chỉnh tier / chốt V1–V7 — sau đó mới scale GDD từng volume.*