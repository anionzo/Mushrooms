# Content schema index — ScriptableObjects & save DTOs

**Source of truth implementation:** types in `Mushroom.Core.Contracts` + SO assets under `Assets/_Game/Data/`.  
**Version:** 0.1

---

## 1. SpeciesDefinition

| Field | Type | Required | Notes |
| --- | --- | --- | --- |
| `speciesId` | string | yes | snake_case unique |
| `displayNameKey` | string | yes | L10N key |
| `familyId` | string | no | Taxonomy |
| `biomeTags` | string[] | no | Filter spawn/shop |
| `rarity` | enum | yes | Common…Event |
| `growthCurveId` | string | yes | ref GrowthCurveDefinition |
| `harvestLootTableId` | string | yes | |
| `moistureSensitivity` | float | no | default 1 |
| `preferredSeasons` | enum[] | Tier C | |
| `preferredTimePhases` | enum[] | Tier C | |
| `mutationRecipeIds` | string[] | Tier C | |
| `addressablePrefabRef` | AssetRef | yes | View |
| `iconRef` | AssetRef | yes | UI |

---

## 2. GrowthCurveDefinition

| Field | Type |
| --- | --- |
| `curveId` | string |
| `stages` | StageEntry[] |

**StageEntry:** `stageId`, `durationSimMinutes`, `spriteStageKey`

---

## 3. PlotState (runtime + save)

| Field | Type |
| --- | --- |
| `plotId` | int |
| `moisture` | float |
| `wilt` | bool (derived or cached) |
| `mushroom` | MushroomInstanceDto? |

---

## 4. MushroomInstanceDto

| Field | Type |
| --- | --- |
| `entityId` | guid string |
| `speciesId` | string |
| `stageId` | string |
| `stageProgress01` | float |

---

## 5. MutationRecipe (Tier C)

| Field | Type |
| --- | --- |
| `recipeId` | string |
| `inputSpeciesId` | string |
| `requiredWeather` | enum? |
| `requiredMoonPhase` | enum? |
| `requiredItems` | ItemStack[] |
| `outputSpeciesId` | string |
| `oneTimePerSave` | bool |

---

## 6. DecorationDefinition

| Field | Type |
| --- | --- |
| `decorationId` | string |
| `footprintCells` | Vector2Int[] |
| `layer` | enum Background/Mid/Fore |
| `addressablePrefabRef` | AssetRef |

---

## 7. ShopOfferTable

| Field | Type |
| --- | --- |
| `tableId` | string |
| `rotation` | Daily/Weekly/Season/Event |
| `entries` | OfferEntry[] |

**OfferEntry:** `itemId`, `priceCoins`, `weight`, `minDay`

---

## 8. Save header v1

| Field | Type |
| --- | --- |
| `saveVersion` | int = 1 |
| `checksum` | string |
| `buildId` | string |
| `contentVersion` | string |
| `lastSimUtc` | ISO8601 |
| `totalSimMinutes` | double |

See `Mushrooms/Docs/SaveSchema/v1.md` for full JSON example.

---

## 9. Validation rules (Editor US-M4-01)

- `speciesId` unique across all SO  
- ≥4 stages per species Tier A  
- `iconRef` not null  
- Loot table resolves  

---

*Expand per GDD Vol 3 when Tier C mutation tables lock.*