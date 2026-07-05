# Test Matrix — Desktop Garden

Maps product behavior to proof. Status **planned** until evidence exists.

## Status Values

| Status | Meaning |
| --- | --- |
| planned | Intended; not implemented |
| in_progress | Building |
| implemented | Proof attached |
| changed | Contract changed |
| retired | Removed |

## Matrix (Tier A / VS1 core)

| Story / Area | Contract | Unit | Integration | E2E | Platform | Status | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| US-M0-04 | Event bus | yes | no | no | no | planned | — |
| US-M0-07 | Game state machine | yes | no | no | no | planned | — |
| US-M2-03 | Growth stages | yes | yes | no | no | planned | — |
| US-M2-10 | Moisture decay/wilt | yes | yes | no | no | planned | — |
| US-M2-11 | Water plot | yes | yes | no | no | planned | — |
| US-M2-07 | Save atomic round-trip | yes | yes | yes | no | planned | — |
| US-M2-08 | Offline 24h cap | yes | no | no | no | planned | — |
| US-M3-04 | Harvest loop | no | yes | yes | no | planned | — |
| US-M3-11 | Water/wilt UX | no | yes | yes | no | planned | — |
| US-M1-04 | Click-through | no | no | yes | yes Win11 | planned | QA matrix |
| VS1 | Full slice | partial | yes | yes | no | planned | VS1 checklist |

## Matrix (Tier B+)

| Story / Area | Contract | Unit | Integration | E2E | Platform | Status | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| US-M5-06 | Economy invariants | yes | yes | yes | no | planned | — |
| US-M6-02 | Weather FSM | yes | yes | no | no | planned | — |
| US-M9-01 | Steam achievements | no | yes | yes | yes | planned | — |

## Evidence Rules

- Unit: `Mushroom.Core.Tests` EditMode.
- Integration: save, pipeline, moisture+growth together.
- E2E: PlayMode or Windows build manual per `docs/QA/`.
- Platform: `docs/QA/DESKTOP_WIN11_MATRIX.md`.

Update row when `harness-cli story update` used (optional).