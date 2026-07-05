# 0008 — Desktop Garden product + Unity monorepo

## Status

accepted

## Context

- Product vision **Desktop Garden** (ecosystem desktop sim, không clone Mushroom Nook).
- Unity project lives at repository path `Mushrooms/` (URP 2D, Unity 6).
- Harness docs, stories, and Khuym state live at repository root.

## Decision

1. **Monorepo:** Single git repo `anionzo/Mushrooms` containing harness + `Mushrooms/` Unity project.
2. **Product codename:** Desktop Garden (working title until marketing lock).
3. **Stack:** Unity 6 LTS (6000.x), C#, URP 2D, JSON save, Win32 desktop integration in M1.
4. **Implementation order:** M0 → M2 → M3 (VS1 with moisture) → M4/M5 → M1 (VS2) → M6–M9 per `GAME_MASTER_PLAN.md`.
5. **Architecture style:** Systems + services + asmdef; avoid monolithic `*Manager` singletons (see `DESKTOP_IDLE_SIM_ARCHITECTURE.md`).

## Consequences

- Root `.gitignore` must exclude `Mushrooms/Library`, `Temp`, `UserSettings`.
- Nested `.git` in Unity folder must not be reintroduced.
- `docs/decisions/0008` supersedes generic “separate MushroomDesktop repo” wording in older plan headers.
- Addressables package must be added before M4 (tracked P0-03b).

## Alternatives considered

- **Separate Unity repo:** clearer CI, but worse doc sync — rejected for solo workflow.
- **Rename folder `_Game` only:** future refactor; current folder name `Mushrooms/` kept for Unity Hub path stability.